---
project: noble-hashes
stars: 610
description: Audited & minimal JS implementation of hash functions, MACs and KDFs.
url: https://github.com/paulmillr/noble-hashes
---

noble-hashes
============

Audited & minimal JS implementation of hash functions, MACs and KDFs.

-   🔒 **Audited** by an independent security firm
-   🔻 Tree-shakeable: unused code is excluded from your builds
-   🏎 Fast: hand-optimized for caveats of JS engines
-   🔍 Reliable: chained / sliding window / DoS tests and fuzzing ensure correctness
-   🔁 No unrolled loops: makes it easier to verify and reduces source code size up to 5x
-   🦘 Includes SHA, RIPEMD, BLAKE, HMAC, HKDF, PBKDF, Scrypt, Argon2 & KangarooTwelve
-   🪶 47KB for everything, 5KB (2.5KB gzipped) for single-hash build

Take a glance at GitHub Discussions for questions and support. The library's initial development was funded by Ethereum Foundation.

### This library belongs to _noble_ cryptography

> **noble cryptography** — high-security, easily auditable set of contained cryptographic libraries and tools.

-   Zero or minimal dependencies
-   Highly readable TypeScript / JS code
-   PGP-signed releases and transparent NPM builds
-   All libraries: ciphers, curves, hashes, post-quantum, 4kb secp256k1 / ed25519
-   Check out homepage for reading resources, documentation and apps built with noble

Usage
-----

> npm install @noble/hashes

We support all major platforms and runtimes. For Deno, ensure to use npm specifier. For React Native, you may need a polyfill for getRandomValues. A standalone file noble-hashes.js is also available.

// import \* from '@noble/hashes'; // Error: use sub-imports, to ensure small app size
import { sha256 } from '@noble/hashes/sha2'; // ECMAScript modules (ESM) and Common.js
// import { sha256 } from 'npm:@noble/hashes@1.3.0/sha2'; // Deno
console.log(sha256(new Uint8Array(\[1, 2, 3\]))); // Uint8Array(32) \[3, 144, 88, 198, 242...\]
// you could also pass strings that will be UTF8-encoded to Uint8Array
console.log(sha256('abc')); // == sha256(new TextEncoder().encode('abc'))

-   Implementations
    -   sha2: sha256, sha384, sha512 and others
    -   sha3: FIPS, SHAKE, Keccak
    -   sha3-addons: cSHAKE, KMAC, K12, M14, TurboSHAKE
    -   ripemd160
    -   blake2b, blake2s, blake3
    -   sha1: legacy hash
    -   hmac
    -   hkdf
    -   pbkdf2
    -   scrypt
    -   argon2
    -   utils
    -   All available imports
-   Security
    -   Constant-timeness
    -   Memory dumping
    -   Supply chain security
    -   Randomness
    -   Quantum computers
-   Speed
-   Contributing & testing
-   License

### Implementations

All hash functions:

-   receive `Uint8Array` and return `Uint8Array`
-   may receive `string`, which is automatically converted to `Uint8Array` via utf8 encoding **(not hex)**
-   support little-endian and big-endian architectures
-   can hash up to 4GB per chunk, with any amount of chunks

function hash(message: Uint8Array | string): Uint8Array;
hash(new Uint8Array(\[1, 3\]));
hash('string') \== hash(new TextEncoder().encode('string'));

All hash functions can be constructed via `hash.create()` method:

-   the result is `Hash` subclass instance, which has `update()` and `digest()` methods
-   `digest()` finalizes the hash and makes it no longer usable

hash
  .create()
  .update(new Uint8Array(\[1, 3\]))
  .digest();

_Some_ hash functions can also receive `options` object, which can be either passed as a:

-   second argument to hash function: `blake3('abc', { key: 'd', dkLen: 32 })`
-   first argument to class initializer: `blake3.create({ context: 'e', dkLen: 32 })`

#### sha2: sha256, sha384, sha512 and others

import { sha256, sha384, sha512, sha224, sha512\_256, sha512\_384 } from '@noble/hashes/sha2';
// also available as aliases:
// import ... from '@noble/hashes/sha256'
// import ... from '@noble/hashes/sha512'

// Variant A:
const h1a \= sha256('abc');

// Variant B:
const h1b \= sha256
  .create()
  .update(Uint8Array.from(\[1, 2, 3\]))
  .digest();

for (let hash of \[sha384, sha512, sha224, sha512\_256, sha512\_384\]) {
  const res1 \= hash('abc');
  const res2 \= hash
    .create()
    .update('def')
    .update(Uint8Array.from(\[1, 2, 3\]))
    .digest();
}

See RFC 4634 and the paper on truncated SHA512/256.

#### sha3: FIPS, SHAKE, Keccak

import {
  sha3\_224,
  sha3\_256,
  sha3\_384,
  sha3\_512,
  keccak\_224,
  keccak\_256,
  keccak\_384,
  keccak\_512,
  shake128,
  shake256,
} from '@noble/hashes/sha3';
const h5a \= sha3\_256('abc');
const h5b \= sha3\_256
  .create()
  .update(Uint8Array.from(\[1, 2, 3\]))
  .digest();
const h6a \= keccak\_256('abc');
const h7a \= shake128('abc', { dkLen: 512 });
const h7b \= shake256('abc', { dkLen: 512 });

See FIPS PUB 202, Website.

Check out the differences between SHA-3 and Keccak

#### sha3-addons: cSHAKE, KMAC, K12, M14, TurboSHAKE

import {
  cshake128,
  cshake256,
  kmac128,
  kmac256,
  k12,
  m14,
  turboshake128,
  turboshake256,
  tuplehash128,
  tuplehash256,
  parallelhash128,
  parallelhash256,
  keccakprg,
} from '@noble/hashes/sha3-addons';
const h7c \= cshake128('abc', { personalization: 'def' });
const h7d \= cshake256('abc', { personalization: 'def' });
const h7e \= kmac128('key', 'message');
const h7f \= kmac256('key', 'message');
const h7h \= k12('abc');
const h7g \= m14('abc');
const h7t1 \= turboshake128('abc');
const h7t2 \= turboshake256('def', { D: 0x05 });
const h7i \= tuplehash128(\['ab', 'c'\]); // tuplehash(\['ab', 'c'\]) !== tuplehash(\['a', 'bc'\]) !== tuplehash(\['abc'\])
// Same as k12/blake3, but without reduced number of rounds. Doesn't speedup anything due lack of SIMD and threading,
// added for compatibility.
const h7j \= parallelhash128('abc', { blockLen: 8 });
// pseudo-random generator, first argument is capacity. XKCP recommends 254 bits capacity for 128-bit security strength.
// \* with a capacity of 254 bits.
const p \= keccakprg(254);
p.feed('test');
const rand1b \= p.fetch(1);

-   Full NIST SP 800-185: cSHAKE, KMAC, TupleHash, ParallelHash + XOF variants
-   Reduced-round Keccak:
    -   🦘 K12 aka KangarooTwelve
    -   M14 aka MarsupilamiFourteen
    -   TurboSHAKE
-   KeccakPRG: Pseudo-random generator based on Keccak

#### ripemd160

import { ripemd160 } from '@noble/hashes/ripemd160';
// function ripemd160(data: Uint8Array): Uint8Array;
const hash8 \= ripemd160('abc');
const hash9 \= ripemd160
  .create()
  .update(Uint8Array.from(\[1, 2, 3\]))
  .digest();

See RFC 2286, Website

#### blake2b, blake2s, blake3

import { blake2b } from '@noble/hashes/blake2b';
import { blake2s } from '@noble/hashes/blake2s';
import { blake3 } from '@noble/hashes/blake3';

const h10a \= blake2s('abc');
const b2params \= { key: new Uint8Array(\[1\]), personalization: t, salt: t, dkLen: 32 };
const h10b \= blake2s('abc', b2params);
const h10c \= blake2s
  .create(b2params)
  .update(Uint8Array.from(\[1, 2, 3\]))
  .digest();

// All params are optional
const h11 \= blake3('abc', { dkLen: 256, key: 'def', context: 'fji' });

See RFC 7693, Website.

#### sha1: legacy hash

SHA1 was cryptographically broken, however, it was not broken for cases like HMAC.

See RFC4226 B.2.

Don't use it for a new protocol.

import { sha1 } from '@noble/hashes/sha1';
const h12 \= sha1('def');

#### hmac

import { hmac } from '@noble/hashes/hmac';
import { sha256 } from '@noble/hashes/sha2';
const mac1 \= hmac(sha256, 'key', 'message');
const mac2 \= hmac
  .create(sha256, Uint8Array.from(\[1, 2, 3\]))
  .update(Uint8Array.from(\[4, 5, 6\]))
  .digest();

Matches RFC 2104.

#### hkdf

import { hkdf } from '@noble/hashes/hkdf';
import { sha256 } from '@noble/hashes/sha2';
import { randomBytes } from '@noble/hashes/utils';
const inputKey \= randomBytes(32);
const salt \= randomBytes(32);
const info \= 'abc';
const dkLen \= 32;
const hk1 \= hkdf(sha256, inputKey, salt, info, dkLen);

// == same as
import \* as hkdf from '@noble/hashes/hkdf';
import { sha256 } from '@noble/hashes/sha2';
const prk \= hkdf.extract(sha256, inputKey, salt);
const hk2 \= hkdf.expand(sha256, prk, info, dkLen);

Matches RFC 5869.

#### pbkdf2

import { pbkdf2, pbkdf2Async } from '@noble/hashes/pbkdf2';
import { sha256 } from '@noble/hashes/sha2';
const pbkey1 \= pbkdf2(sha256, 'password', 'salt', { c: 32, dkLen: 32 });
const pbkey2 \= await pbkdf2Async(sha256, 'password', 'salt', { c: 32, dkLen: 32 });
const pbkey3 \= await pbkdf2Async(sha256, Uint8Array.from(\[1, 2, 3\]), Uint8Array.from(\[4, 5, 6\]), {
  c: 32,
  dkLen: 32,
});

Matches RFC 2898.

#### scrypt

import { scrypt, scryptAsync } from '@noble/hashes/scrypt';
const scr1 \= scrypt('password', 'salt', { N: 2 \*\* 16, r: 8, p: 1, dkLen: 32 });
const scr2 \= await scryptAsync('password', 'salt', { N: 2 \*\* 16, r: 8, p: 1, dkLen: 32 });
const scr3 \= await scryptAsync(Uint8Array.from(\[1, 2, 3\]), Uint8Array.from(\[4, 5, 6\]), {
  N: 2 \*\* 17,
  r: 8,
  p: 1,
  dkLen: 32,
  onProgress(percentage) {
    console.log('progress', percentage);
  },
  maxmem: 2 \*\* 32 + 128 \* 8 \* 1, // N \* r \* p \* 128 + (128\*r\*p)
});

Conforms to RFC 7914, Website

-   `N, r, p` are work factors. To understand them, see the blog post. `r: 8, p: 1` are common. JS doesn't support parallelization, making increasing p meaningless.
-   `dkLen` is the length of output bytes e.g. `32` or `64`
-   `onProgress` can be used with async version of the function to report progress to a user.
-   `maxmem` prevents DoS and is limited to `1GB + 1KB` (`2**30 + 2**10`), but can be adjusted using formula: `N * r * p * 128 + (128 * r * p)`

Time it takes to derive Scrypt key under different values of N (2\*\*N) on Apple M2 (mobile phones can be 1x-4x slower):

N pow

Time

16

0.17s

17

0.35s

18

0.7s

19

1.4s

20

2.9s

21

5.6s

22

11s

23

26s

24

56s

Note

We support N larger than `2**20` where available, however, not all JS engines support >= 2GB ArrayBuffer-s. When using such N, you'll need to manually adjust `maxmem`, using formula above. Other JS implementations don't support large N-s.

#### argon2

import { argon2d, argon2i, argon2id } from '@noble/hashes/argon2';
const result \= argon2id('password', 'saltsalt', { t: 2, m: 65536, p: 1, maxmem: 2 \*\* 32 \- 1 });

Argon2 RFC 9106 implementation.

Warning

Argon2 can't be fast in JS, because there is no fast Uint64Array. It is suggested to use Scrypt instead. Being 5x slower than native code means brute-forcing attackers have bigger advantage.

#### utils

import { bytesToHex as toHex, randomBytes } from '@noble/hashes/utils';
console.log(toHex(randomBytes(32)));

-   `bytesToHex` will convert `Uint8Array` to a hex string
-   `randomBytes(bytes)` will produce cryptographically secure random `Uint8Array` of length `bytes`

#### All available imports

import { sha256, sha384, sha512, sha224, sha512\_256, sha512\_384 } from '@noble/hashes/sha2';
// prettier-ignore
import {
  sha3\_224, sha3\_256, sha3\_384, sha3\_512,
  keccak\_224, keccak\_256, keccak\_384, keccak\_512,
  shake128, shake256
} from '@noble/hashes/sha3';
// prettier-ignore
import {
  cshake128, cshake256,
  turboshake128, turboshake256,
  kmac128, kmac256,
  tuplehash256, parallelhash256,
  k12, m14, keccakprg
} from '@noble/hashes/sha3-addons';
import { ripemd160 } from '@noble/hashes/ripemd160';
import { blake3 } from '@noble/hashes/blake3';
import { blake2b } from '@noble/hashes/blake2b';
import { blake2s } from '@noble/hashes/blake2s';
import { hmac } from '@noble/hashes/hmac';
import { hkdf } from '@noble/hashes/hkdf';
import { pbkdf2, pbkdf2Async } from '@noble/hashes/pbkdf2';
import { scrypt, scryptAsync } from '@noble/hashes/scrypt';

import { sha1 } from '@noble/hashes/sha1'; // legacy

// small utility method that converts bytes to hex
import { bytesToHex as toHex } from '@noble/hashes/utils';
console.log(toHex(sha256('abc'))); // ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad

Security
--------

The library has been independently audited:

-   at version 1.0.0, in Jan 2022, by Cure53
    -   PDFs: website, in-repo
    -   Changes since audit.
    -   Scope: everything, besides `blake3`, `sha3-addons`, `sha1` and `argon2`, which have not been audited
    -   The audit has been funded by Ethereum Foundation with help of Nomic Labs

It is tested against property-based, cross-library and Wycheproof vectors, and has fuzzing by Guido Vranken's cryptofuzz.

If you see anything unusual: investigate and report.

### Constant-timeness

_JIT-compiler_ and _Garbage Collector_ make "constant time" extremely hard to achieve timing attack resistance in a scripting language. Which means _any other JS library can't have constant-timeness_. Even statically typed Rust, a language without GC, makes it harder to achieve constant-time for some cases. If your goal is absolute security, don't use any JS lib — including bindings to native ones. Use low-level libraries & languages. Nonetheless we're targetting algorithmic constant time.

### Memory dumping

The library shares state buffers between hash function calls. The buffers are zeroed-out after each call. However, if an attacker can read application memory, you are doomed in any case:

-   At some point, input will be a string and strings are immutable in JS: there is no way to overwrite them with zeros. For example: deriving key from `scrypt(password, salt)` where password and salt are strings
-   Input from a file will stay in file buffers
-   Input / output will be re-used multiple times in application which means it could stay in memory
-   `await anything()` will always write all internal variables (including numbers) to memory. With async functions / Promises there are no guarantees when the code chunk would be executed. Which means attacker can have plenty of time to read data from memory
-   There is no way to guarantee anything about zeroing sensitive data without complex tests-suite which will dump process memory and verify that there is no sensitive data left. For JS it means testing all browsers (incl. mobile), which is complex. And of course it will be useless without using the same test-suite in the actual application that consumes the library

### Supply chain security

-   **Commits** are signed with PGP keys, to prevent forgery. Make sure to verify commit signatures.
-   **Releases** are transparent and built on GitHub CI. Make sure to verify provenance logs
-   **Rare releasing** is followed to ensure less re-audit need for end-users
-   **Dependencies** are minimized and locked-down:
    -   If your app has 500 dependencies, any dep could get hacked and you'll be downloading malware with every install. We make sure to use as few dependencies as possible
    -   We prevent automatic dependency updates by locking-down version ranges. Every update is checked with `npm-diff`
-   **Dev Dependencies** are only used if you want to contribute to the repo. They are disabled for end-users:
    -   scure-base, scure-bip32, scure-bip39, micro-bmark and micro-should are developed by the same author and follow identical security practices
    -   prettier (linter), fast-check (property-based testing) and typescript are used for code quality, vector generation and ts compilation. The packages are big, which makes it hard to audit their source code thoroughly and fully

### Randomness

We're deferring to built-in crypto.getRandomValues which is considered cryptographically secure (CSPRNG).

In the past, browsers had bugs that made it weak: it may happen again. Implementing a userspace CSPRNG to get resilient to the weakness is even worse: there is no reliable userspace source of quality entropy.

### Quantum computers

Cryptographically relevant quantum computer, if built, will allow to utilize Grover's algorithm to break hashes in 2^n/2 operations, instead of 2^n.

This means SHA256 should be replaced with SHA512, SHA3-256 with SHA3-512, SHAKE128 with SHAKE256 etc.

Australian ASD prohibits SHA256 and similar hashes after 2030.

Speed
-----

```
npm run bench
```

Benchmarks measured on Apple M2 with node v22.

```
32B
sha256 x 1,377,410 ops/sec @ 726ns/op
sha384 x 518,403 ops/sec @ 1μs/op
sha512 x 518,941 ops/sec @ 1μs/op
sha3_256 x 188,608 ops/sec @ 5μs/op
sha3_512 x 190,114 ops/sec @ 5μs/op
k12 x 324,254 ops/sec @ 3μs/op
m14 x 286,204 ops/sec @ 3μs/op
blake2b x 352,236 ops/sec @ 2μs/op
blake2s x 586,510 ops/sec @ 1μs/op
blake3 x 681,198 ops/sec @ 1μs/op
ripemd160 x 1,275,510 ops/sec @ 784ns/op

1MB
sha256 x 197 ops/sec @ 5ms/op
sha384 x 86 ops/sec @ 11ms/op
sha512 x 86 ops/sec @ 11ms/op
sha3_256 x 25 ops/sec @ 39ms/op
sha3_512 x 13 ops/sec @ 74ms/op
k12 x 58 ops/sec @ 17ms/op
m14 x 41 ops/sec @ 24ms/op
blake2b x 50 ops/sec @ 19ms/op
blake2s x 44 ops/sec @ 22ms/op
blake3 x 57 ops/sec @ 17ms/op
ripemd160 x 193 ops/sec @ 5ms/op

# MAC
hmac(sha256) x 404,203 ops/sec @ 2μs/op
hmac(sha512) x 137,136 ops/sec @ 7μs/op
kmac256 x 58,799 ops/sec @ 17μs/op
blake3(key) x 619,962 ops/sec @ 1μs/op

# KDF
hkdf(sha256) x 180,538 ops/sec @ 5μs/op
blake3(context) x 336,247 ops/sec @ 2μs/op
pbkdf2(sha256, c: 2 ** 18) x 3 ops/sec @ 292ms/op
pbkdf2(sha512, c: 2 ** 18) x 1 ops/sec @ 920ms/op
scrypt(n: 2 ** 18, r: 8, p: 1) x 1 ops/sec @ 605ms/op
argon2id(t: 1, m: 256MB) x 0 ops/sec @ 4021ms/op
```

Compare to native node.js implementation that uses C bindings instead of pure-js code:

```
SHA256 32B node x 1,302,083 ops/sec @ 768ns/op
SHA384 32B node x 975,609 ops/sec @ 1μs/op
SHA512 32B node x 983,284 ops/sec @ 1μs/op
SHA3-256 32B node x 910,746 ops/sec @ 1μs/op
# keccak, k12, m14 are not implemented
BLAKE2b 32B node x 967,117 ops/sec @ 1μs/op
BLAKE2s 32B node x 1,055,966 ops/sec @ 947ns/op
# BLAKE3 is not implemented
RIPEMD160 32B node x 1,002,004 ops/sec @ 998ns/op
HMAC-SHA256 32B node x 919,963 ops/sec @ 1μs/op
HKDF-SHA256 32 node x 369,276 ops/sec @ 2μs/op
PBKDF2-HMAC-SHA256 262144 node x 25 ops/sec @ 39ms/op
PBKDF2-HMAC-SHA512 262144 node x 7 ops/sec @ 132ms/op
Scrypt r: 8, p: 1, n: 262144 node x 1 ops/sec @ 523ms/op
```

It is possible to make this library 4x+ faster by _doing code generation of full loop unrolls_. We've decided against it. Reasons:

-   the library must be auditable, with minimum amount of code, and zero dependencies
-   most method invocations with the lib are going to be something like hashing 32b to 64kb of data
-   hashing big inputs is 10x faster with low-level languages, which means you should probably pick 'em instead

The current performance is good enough when compared to other projects; SHA256 takes only 900 nanoseconds to run.

Contributing & testing
----------------------

`test/misc` directory contains implementations of loop unrolling and md5.

-   `npm install && npm run build && npm test` will build the code and run tests.
-   `npm run lint` / `npm run format` will run linter / fix linter issues.
-   `npm run bench` will run benchmarks, which may need their deps first (`npm run bench:install`)
-   `cd build && npm install && npm run build:release` will build single file
-   There is **additional** 20-min DoS test `npm run test:dos` and 2-hour "big" multicore test `npm run test:big`. See our approach to testing

Check out github.com/paulmillr/guidelines for general coding practices and rules.

See paulmillr.com/noble for useful resources, articles, documentation and demos related to the library.

License
-------

The MIT License (MIT)

Copyright (c) 2022 Paul Miller (https://paulmillr.com)

See LICENSE file.
