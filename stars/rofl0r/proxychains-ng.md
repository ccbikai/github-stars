---
project: proxychains-ng
stars: 9842
description: proxychains ng (new generation) - a preloader which hooks calls to sockets in dynamically linked programs and redirects it through one or more socks/http proxies. continuation of the unmaintained proxychains project. the sf.net page is currently not updated, use releases from github release page instead.
---

ProxyChains-NG ver 4.17 README
=============================

  ProxyChains is a UNIX program, that hooks network-related libc functions
  in DYNAMICALLY LINKED programs via a preloaded DLL (dlsym(), LD\_PRELOAD)
  and redirects the connections through SOCKS4a/5 or HTTP proxies.
  It supports TCP only (no UDP/ICMP etc).

  The way it works is basically a HACK; so it is possible that it doesn't
  work with your program, especially when it's a script, or starts
  numerous processes like background daemons or uses dlopen() to load
  "modules" (bug in glibc dynlinker).
  It should work with simple compiled (C/C++) dynamically linked programs
  though.

  If your program doesn't work with proxychains, consider using an
  iptables based solution instead; this is much more robust.

  Supported Platforms: Linux, BSD, Mac, Haiku.


\*\*\*\*\*\*\*\*\*\*\* ATTENTION \*\*\*\*\*\*\*\*\*\*\*

  this program can be used to circumvent censorship.
  doing so can be VERY DANGEROUS in certain countries.

  ALWAYS MAKE SURE THAT PROXYCHAINS WORKS AS EXPECTED
  BEFORE USING IT FOR ANYTHING SERIOUS.

  this involves both the program and the proxy that you're going to
  use.

  for example, you can connect to some "what is my ip" service
  like ifconfig.me to make sure that it's not using your real ip.

  ONLY USE PROXYCHAINS IF YOU KNOW WHAT YOU'RE DOING.

  THE AUTHORS AND MAINTAINERS OF PROXYCHAINS DO NOT TAKE ANY
  RESPONSIBILITY FOR ANY ABUSE OR MISUSE OF THIS SOFTWARE AND
  THE RESULTING CONSEQUENCES.

\*\*\* Installation \*\*\*

  # needs a working C compiler, preferably gcc
  ./configure --prefix=/usr --sysconfdir=/etc
  make
  \[optional\] sudo make install
  \[optional\] sudo make install-config (installs proxychains.conf)

  if you dont install, you can use proxychains from the build directory
  like this: ./proxychains4 -f src/proxychains.conf telnet google.com 80

Changelog:
----------
Version 4.17
- add hook for close\_range function, fixing newer versions of openssh
- fat-binary-m1 option for mac
- fix DNS error handling in proxy\_dns\_old
- simplify init code
- fix openbsd preloading
- fix double-close in multithreaded apps
- various improvements to configure script

Version 4.16
- fix regression in configure script linker flag detection
- remove 10 year old workaround for wrong glibc getnameinfo signature
- support for new DYLD hooking method for OSX Monterey
- netbsd compilation fix
- support IPv6 localnets
- more user-friendly error message when execvp fails
- proxy\_getaddrinfo(): fill in ai\_socktype if requested

Version 4.15
- fix configure script for buggy binutils version
- initialize rand\_seed with nano-second granularity
- add support for numeric ipv6 in getaddrinfo
- fix bug in getaddrinfo when node is null and !passive
- add dnat feature
- add raw proxy type
- add haiku support
- add proxy\_dns\_old to emulate proxychains 3.1 behaviour
- add new proxy\_dns\_daemon feature (experimental)
- various other fixes

Version 4.14
- allow alternative proto://user:pass@ip:port syntax for proxylist
- fix endless loop in round robin mode when all proxies are down (#147)
- fix compilation on android (#265)
- fix fd leak in forked processes (#273)
- skip connection attempt to nullrouted ips
- allow hostnames for proxylist under specific circumstances

Version 4.13
- fix robustness of DNS lookup thread and a segfault
- fix socks5 user/pass auth on non-conforming servers
- fix memory leak
- add support for Solaris

Version 4.12
- fix several build issues
  - for MAC
  - with -pie
  - with custom CC
- compatibility fix for some GUI apps (8870140)
- compatibility fix for some HTTP proxies (cf9a16d)
- fix several warnings for cleaner build on debian
- fix random\_chain on OSX (0f6b226)

Version 4.11
- preliminary IPv6 support
- fixed bug in hostsreader
- preliminary support for usage on OpenBSD (caveat emptor)

Version 4.10
- fix regression in linking order with custom LDFLAGS
- fix segfault in DNS mapping code in programs with > ~400 different lookups

Version 4.9
- fix a security issue CVE-2015-3887
- add sendto hook to handle MSG\_FASTOPEN flag
- replace problematic hostentdb with hostsreader
- fix compilation on OpenBSD (although doesn't work there)

Version 4.8.1:
- fix regression in 4.8 install-config Makefile target

Version 4.8:
- fix for odd cornercase where getaddrinfo was used with AI\_NUMERICHOST
  to test for a numeric ip instead of resolving it (fixes nmap).
- allow usage with programs that rely on LD\_PRELOAD themselves
- reject wrong entries in config file
- print version number on startup

Version 4.7:
- new round\_robin chaintype by crass.
- fix bug with lazy allocation when GCC constructor was not used.
- new configure flag --fat-binary to create a "fat" binary/library on OS X
- return EBADF rather than EINTR in close hook.
  it's legal for a program to retry close() calls when they receive
  EINTR, which could cause an infinite loop, as seen in chromium.

Version 4.6:
- some cosmetic fixes to Makefile, fix a bug when non-numeric ip was
  used as proxy server address.

Version 4.5:
- hook close() to prevent OpenSSH from messing with internal infrastructure.
  this caused ssh client to segfault when proxified.

Version 4.4:
- FreeBSD port
- fixes some installation issues on Debian and Mac.

Version 4.3:
- fixes programs that do dns-lookups in child processes (fork()ed),
  like irssi. to achieve this, support for compilation without pthreads
  was sacrified.
- fixes thread safety for gethostent() calls.
- improved DNS handling speed, since hostent db is cached.

Version 4.2:
- fixes compilation issues with ubuntu 12.04 toolchain
- fixes segfault in rare codepath

Version 4.1
- support for mac os x (all archs)
- all internal functions are threadsafe when compiled with -DTHREAD\_SAFE
  (default).

Version 4.0
- replaced dnsresolver script (which required a dynamically linked "dig"
  binary to be present) with remote DNS lookup.
  this speeds up any operation involving DNS, as the old script had to use TCP.
  additionally it allows to use .onion urls when used with TOR.
- removed broken autoconf build system with a simple Makefile.
  there's a ./configure script though for convenience.
  it also adds support for a config file passed via command line switches/
  environment variables.

Version 3.0
- support for DNS resolving through proxy
  supports SOCKS4, SOCKS5 and HTTP CONNECT proxy servers.
  Auth-types: socks - "user/pass" , http - "basic".

When to use it ?
1) When the only way to get "outside" from your LAN is through proxy server.
2) To get out from behind restrictive firewall which filters outgoing ports.
3) To use two (or more) proxies in chain:
	like: your\_host <--> proxy1 <--> proxy2 <--> target\_host
4) To "proxify" some program with no proxy support built-in (like telnet)
5) Access intranet from outside via proxy.
6) To use DNS behind proxy.
7) To access hidden tor onion services.

Some cool features:

\* This program can mix different proxy types in the same chain
	like: your\_host <-->socks5 <--> http <--> socks4 <--> target\_host
\* Different chaining options supported
	random order from the list ( user defined length of chain ).
	exact order  (as they appear in the list )
	dynamic order (smart exclude dead proxies from chain)
\* You can use it with most TCP client applications, possibly even network
	scanners, as long as they use standard libc functionality.
	pcap based scanning does not work.
\* You can use it with servers, like squid, sendmail, or whatever.
\* DNS resolving through proxy.


Configuration:
--------------

proxychains looks for config file in following order:
1)	file listed in environment variable PROXYCHAINS\_CONF\_FILE or
	provided as a -f argument to proxychains script or binary.
2)	./proxychains.conf
3)	$(HOME)/.proxychains/proxychains.conf
4)	$(sysconfdir)/proxychains.conf  \*\*

\*\* usually /etc/proxychains.conf

Usage Example:

	$ proxychains telnet targethost.com

in this example it will run telnet through proxy(or chained proxies)
specified by proxychains.conf

Usage Example:

	$ proxychains -f /etc/proxychains-other.conf telnet targethost2.com

in this example it will use different configuration file then proxychains.conf
to connect to targethost2.com host.

Usage Example:

	$ proxyresolv targethost.com

in this example it will resolve targethost.com through proxy(or chained proxies)
specified by proxychains.conf

Known Problems:
---------------
- newer versions of nmap try to determine the network interface to use
  even if it's not needed (like when doing simple syn scans which use the
  standard POSIX socket API. this results in errors when proxychains hands
  out an ip address to a reserved address space.
  possible workarounds: disable proxy\_dns, use a numeric ip, or use nmap's
  native support for SOCKS proxies.

- Mac OS X 10.11 (El Capitan) ships with a new security feature called SIP
  that prevents hooking of system apps.
  workarounds are to partially disable SIP by issuing
  csrutil enable --without debug in recovery mode,
  or to copy the system binary into the home directory and run it from there.
  see github issue #78 for details.

- the glibc dynlinker has a bug or security feature that inhibits dlopen()ed
  modules from being subject to the same dlsym hooks as installed for the main
  program. this mainly affects scripting languages such as perl or python
  that heavily rely on dlopen() for modules written in C to work.
  there are unconfirmed reports that it works as root though.
  musl libc is unaffected from the bug.


Community:
----------
#proxychains on irc.libera.chat

Donations:
----------
bitcoins donations are welcome - please send to this address:
1C9LBpuy56veBqw5N33sZMoZW8mwCw3tPh