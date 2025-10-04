---
project: upyo
stars: 445
description: |-
    Upyo is a simple and cross-runtime library for sending email messages using SMTP and various email providers.  It works on Node.js, Deno, Bun, and edge functions.
url: https://github.com/dahlia/upyo
---

<!-- deno-fmt-ignore-file -->

<img src="docs/public/logo.svg" width="128" height="128" align="right">

Upyo
====

Upyo is a cross-runtime email library that provides a unified, type-safe API
for sending emails across Node.js, Deno, Bun, and edge functions. Switch
between SMTP and HTTP-based providers (Mailgun, Resend, SendGrid, Amazon SES)
without changing your application code, while enjoying full TypeScript support,
consistent error handling, and built-in testing capabilities with mock
transports across all runtimes.

Here's a quick demo of sending an email using the Mailgun transport:

~~~~ typescript
import { createMessage } from "@upyo/core";
import { MailgunTransport } from "@upyo/mailgun";
import fs from "node:fs/promises";
import process from "node:process";

const message = createMessage({
  from: "sender@example.com",
  to: "recipient@example.net",
  subject: "Hello from Upyo!",
  content: { text: "This is a test email." },
  attachments: [
    new File(
      [await fs.readFile("image.jpg"), "image.jpg", { type: "image/jpeg" }]
    )
  ],
});

const transport = new MailgunTransport({
  apiKey: process.env.MAILGUN_KEY!,
  domain: process.env.MAILGUN_DOMAIN!,
  region: process.env.MAILGUN_REGION as "us" | "eu",
});

const receipt = await transport.send(message);
if (receipt.successful) {
  console.log("Message sent with ID:", receipt.messageId);
} else {
  console.error("Send failed:", receipt.errorMessages.join(", "));
}
~~~~


Docs
----

Upyo provides comprehensive documentation to help you get started quickly:
<https://upyo.org/>.

API reference documentation for each package is available on JSR (see below).


Packages
--------

Upyo is a monorepo which contains several packages.  The main package is
*@upyo/core*, which provides the shared types and common interfaces for
sending email messages.  Other packages implement specific transports for
sending messages.  The following is a list of the available packages:

| Package                                         | JSR                            | npm                            | Description                                        |
| ----------------------------------------------- | ------------------------------ | ------------------------------ | -------------------------------------------------- |
| [@upyo/core](/packages/core/)                   | [JSR][jsr:@upyo/core]          | [npm][npm:@upyo/core]          | Shared types and interfaces for email messages     |
| [@upyo/smtp](/packages/smtp/)                   | [JSR][jsr:@upyo/smtp]          | [npm][npm:@upyo/smtp]          | SMTP transport                                     |
| [@upyo/mailgun](/packages/mailgun/)             | [JSR][jsr:@upyo/mailgun]       | [npm][npm:@upyo/mailgun]       | [Mailgun] transport                                |
| [@upyo/plunk](/packages/plunk/)                 | [JSR][jsr:@upyo/plunk]         | [npm][npm:@upyo/plunk]         | [Plunk] transport                                  |
| [@upyo/resend](/packages/resend/)               | [JSR][jsr:@upyo/resend]        | [npm][npm:@upyo/resend]        | [Resend] transport                                 |
| [@upyo/sendgrid](/packages/sendgrid/)           | [JSR][jsr:@upyo/sendgrid]      | [npm][npm:@upyo/sendgrid]      | [SendGrid] transport                               |
| [@upyo/ses](/packages/ses/)                     | [JSR][jsr:@upyo/ses]           | [npm][npm:@upyo/ses]           | [Amazon SES] transport                             |
| [@upyo/opentelemetry](/packages/opentelemetry/) | [JSR][jsr:@upyo/opentelemetry] | [npm][npm:@upyo/opentelemetry] | [OpenTelemetry] observability  for Upyo transports |
| [@upyo/mock](/packages/mock/)                   | [JSR][jsr:@upyo/mock]          | [npm][npm:@upyo/mock]          | Mock transport for testing                         |

[jsr:@upyo/core]: https://jsr.io/@upyo/core
[npm:@upyo/core]: https://www.npmjs.com/package/@upyo/core
[jsr:@upyo/smtp]: https://jsr.io/@upyo/smtp
[npm:@upyo/smtp]: https://www.npmjs.com/package/@upyo/smtp
[jsr:@upyo/mailgun]: https://jsr.io/@upyo/mailgun
[npm:@upyo/mailgun]: https://www.npmjs.com/package/@upyo/mailgun
[jsr:@upyo/plunk]: https://jsr.io/@upyo/plunk
[npm:@upyo/plunk]: https://www.npmjs.com/package/@upyo
[jsr:@upyo/resend]: https://jsr.io/@upyo/resend
[npm:@upyo/resend]: https://www.npmjs.com/package/@upyo
[jsr:@upyo/sendgrid]: https://jsr.io/@upyo/sendgrid
[npm:@upyo/sendgrid]: https://www.npmjs.com/package/@upyo/sendgrid
[jsr:@upyo/ses]: https://jsr.io/@upyo/ses
[npm:@upyo/ses]: https://www.npmjs.com/package/@upyo/ses
[jsr:@upyo/opentelemetry]: https://jsr.io/@upyo/opentelemetry
[npm:@upyo/opentelemetry]: https://www.npmjs.com/package/@upyo/opentelemetry
[jsr:@upyo/mock]: https://jsr.io/@upyo/mock
[npm:@upyo/mock]: https://www.npmjs.com/package/@upyo/mock
[Mailgun]: https://www.mailgun.com/
[Plunk]: https://www.useplunk.com/
[Resend]: https://resend.com/
[SendGrid]: https://sendgrid.com/
[Amazon SES]: https://aws.amazon.com/ses/
[OpenTelemetry]: https://opentelemetry.io/


Etymology
---------

The name <q>Upyo</q> (pronounced /oo-pee-oh/) is derived from the Korean word
<q>郵票</q> (upyo), which means *postage stamp*.  It reflects the library's
purpose of sending email messages, similar to how a postage stamp is used to
send physical mail.

