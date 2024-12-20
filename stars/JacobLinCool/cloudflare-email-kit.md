---
project: cloudflare-email-kit
stars: 25
description: The Cloudflare Email Kit is a powerful toolkit designed to handle both incoming and outgoing emails with ease on Cloudflare Workers, providing developers with a modular approach to integrating email functionalities within serverless applications.
url: https://github.com/JacobLinCool/cloudflare-email-kit
---

Cloudflare Email Kit
====================

The Cloudflare Email Kit is a powerful toolkit designed to handle both incoming and outgoing emails with ease on Cloudflare Workers. It emphasizes ease of use and composability, providing developers with a modular approach to integrating email functionalities within their serverless applications.

Features
--------

-   **User-Friendly Middleware:** Employ an intuitive middleware system that streamlines email processing.
-   **Composable Routing:** Craft complex email handling logic with a highly composable EmailRouter.
-   **Cloudflare Integrations:** Store emails effortlessly with Cloudflare’s R2 Object Storage and D1 Database support.
-   **Workload Management:** Utilize Cloudflare Queues to efficiently distribute email processing tasks.
-   **Email Utilities:** Simplify the art of parsing, crafting and sending emails with a set of convenient utilities.

Getting Started
---------------

Begin using the Cloudflare Email Kit with a simple installation:

pnpm install cloudflare-email

> The `cloudflare-email` package contains the core functionalities of the Cloudflare Email Kit. For additional features, install the packages listed in the documentation.

Examples
--------

### Router

Navigate the complexities of email routing with customizable rules and actions.

See examples/router.

See the example code

import { CATCH\_ALL, EmailKit, EmailRouter, REJECT\_ALL, SizeGuard, respond } from "cloudflare-email";
import { Backup } from "cloudflare-email-backup";

export interface Env {
    R2: R2Bucket;
    D1: D1Database;
    NOTIFICATION\_EMAIL: string;
}

export default {
    async email(message: ForwardableEmailMessage, env: Env, ctx: ExecutionContext): Promise<void\> {
        const router \= new EmailRouter()
            // handle auto-sent emails
            .match(
                (m) \=> m.isAuto(),
                (m) \=> m.forward(env.NOTIFICATION\_EMAIL),
            )
            // use a sub-router to handle subdomain emails
            .match(
                /@test\\.csie\\.cool$/,
                new EmailRouter()
                    .match(/^admin@/, async (message) \=> {
                        const msg \= respond(message);
                        msg.addMessage({
                            contentType: "text/plain",
                            data: "Hello, I'm the admin!",
                        });
                        await message.reply(msg);
                    })
                    .match(
                        // function matchers are also supported, even async ones which query databases
                        (m) \=> m.from.length % 2 \=== 0,
                        async (message) \=> {
                            const msg \= respond(message);
                            msg.addMessage({
                                contentType: "text/plain",
                                data: \`The length of your email address is even!\`,
                            });
                            await message.reply(msg);
                        },
                    )
                    .match(CATCH\_ALL, async (message) \=> {
                        const msg \= respond(message);
                        msg.addMessage({
                            contentType: "text/plain",
                            data: "The length of your email address is odd!",
                        });
                        await message.reply(msg);
                    }),
            )
            .match(...REJECT\_ALL("Your email is rejected! :P"));

        const kit \= new EmailKit()
            .use(new SizeGuard(10 \* 1024 \* 1024))
            .use(
                new Backup({
                    bucket: env.R2,
                    prefix: "backup",
                    database: env.D1,
                    table: "emails",
                }),
            )
            .use(router);

        await kit.process(message);
    },
};

### Parser

Effortlessly parse and interact with email content and attachments.

See examples/parser.

See the example code

import { EmailKit, SizeGuard, respond } from "cloudflare-email";
import { ParsedContext, Parser } from "cloudflare-email-parser";

export interface Env {
    R2: R2Bucket;
}

export default {
    async email(message: ForwardableEmailMessage, env: Env): Promise<void\> {
        const kit \= new EmailKit()
            .use(new SizeGuard(10 \* 1024 \* 1024))
            .use(new Parser())
            .use({
                name: "save-attechments",
                async handle(ctx: ParsedContext) {
                    for (const attachment of ctx.parsed.attachments) {
                        const { filename, content, mimeType } \= attachment;
                        const key \= \`attachments/${ctx.parsed.messageId}/${filename}\`;
                        console.log(\`Saving attachment ${filename} to ${key} ...\`);
                        await env.R2.put(key, content, {
                            customMetadata: { mime: mimeType },
                        });
                        console.log(\`Saved attachment ${filename} to ${key}.\`);
                    }

                    const res \= respond(ctx.message);
                    res.addMessage({
                        contentType: "text/plain",
                        data: \`${ctx.parsed.attachments.length} attachments saved.\`,
                    });
                    await ctx.message.reply(res);
                },
            });

        await kit.process(message);
    },
};

### Cloudflare Queues

Leverage Cloudflare Queues to get more CPU time (15 minutes instead of 30 seconds) to process emails.

See examples/cloudflare-queues.

See the example code

import { EmailKit, EmailRouter, SizeGuard, respond } from "cloudflare-email";
import { Backup } from "cloudflare-email-backup";
import { EmailQueue, EmailQueueMessage } from "cloudflare-email-queue";

export interface Env {
    R2: R2Bucket;
    D1: D1Database;
    FIRST: Queue<EmailQueueMessage\>;
    SECOND: Queue<EmailQueueMessage\>;
}

export default {
    // receive email, perform size check, and enqueue it to the coresponding queue
    async email(message: ForwardableEmailMessage, env: Env): Promise<void\> {
        const router \= new EmailRouter()
            .match(/@first\\.csie\\.cool$/, new EmailQueue(env.FIRST))
            .match(/@second\\.csie\\.cool$/, new EmailQueue(env.SECOND));

        const kit \= new EmailKit()
            .use(new SizeGuard(10 \* 1024 \* 1024))
            .use(
                new Backup({
                    bucket: env.R2,
                    prefix: "backup",
                    database: env.D1,
                    table: "emails",
                }),
            )
            .use(router);

        await kit.process(message);
    },
    // checkout the queued messages and process them
    async queue(batch: MessageBatch<EmailQueueMessage\>, env: Env) {
        const backup \= new Backup({
            bucket: env.R2,
            prefix: "backup",
            database: env.D1,
            table: "emails",
        });

        // retrieve and re-construct the message
        const retrieve \= async (m: EmailQueueMessage) \=> {
            const raw \= await backup.retrieve(m.message\_id, m.from, m.to);
            if (!raw) {
                throw new Error("Cannot retrieve message.");
            }
            return EmailQueue.retrieve(m, raw);
        };

        if (batch.queue \=== "kit-example-first-email-queue") {
            for (const m of batch.messages) {
                const message \= await retrieve(m.body);

                await new EmailKit()
                    .use(async (ctx) \=> {
                        const reply \= respond(ctx.message);
                        reply.addMessage({
                            contentType: "text/plain",
                            data: "Greeting from first domain.",
                        });
                        await ctx.message.reply(reply);
                    })
                    .handle({ message });

                m.ack();
            }
        } else if (batch.queue \=== "kit-example-second-email-queue") {
            for (const m of batch.messages) {
                const message \= await retrieve(m.body);

                await new EmailKit()
                    .use(async (ctx) \=> {
                        const reply \= respond(ctx.message);
                        reply.addMessage({
                            contentType: "text/plain",
                            data: "Greeting from second domain.",
                        });

                        await ctx.message.reply(reply);
                    })
                    .handle({ message });

                m.ack();
            }
        }
    },
};

Documentation
-------------

Dive into the full potential of the Cloudflare Email Kit by visiting the Documentation.

Join the Community
------------------

We welcome your contributions! To collaborate, fork the repository and submit your pull requests.

Need Help?
----------

Encountered a snag? Have a suggestion? Open an issue on the GitHub issues page.
