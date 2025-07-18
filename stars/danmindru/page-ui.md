---
project: page-ui
stars: 1479
description: |-
    📃 Landing page UI components for React & Next.js, built on top of TailwindCSS
url: https://github.com/danmindru/page-ui
---

> 🆕 New! Get an entire website from a prompt. Including design! Try it out at [pageai.pro](https://pageai.pro) 🚀

# Page UI 📃

[![Page UI CLI version](https://img.shields.io/npm/v/@page-ui/wizard?label=cli&style=flat)](https://github.com/danmindru/page-ui/tree/master/packages/cli)

**Landing page components & templates that you can copy 📋 & paste 🍝**<br/>
[pageui.dev](https://pageui.dev)

A collection of **free templates**, components and examples to create beautiful,
high-converting landing pages with React and Next.js. Open source & themeable
with Tailwind CSS. Inspired by [Shadcn UI](https://ui.shadcn.com/).

Quick links:
- [📀 Installation](https://pageui.shipixen.com/docs/installation)
- [📄 Templates](https://shipixen.com/demo/landing-page-templates)
- [👩‍💻 A ton of demos](https://shipixen.com/demo/landing-page-component-examples)

[Read more](https://pageui.dev/docs/introduction) about Page UI.

> ⚠️ Page UI currently works with Tailwind v3. We are working on adding support for v4.

## 🎨 Templates

[![Specta - A landing page template for a creator platform, featuring a marquee section and a showcase section](https://github.com/user-attachments/assets/e2cc026a-70eb-4b07-a20a-3b2128b90056)](https://shipixen.com/demo/landing-page-templates/template/specta)
[![Gnomie AI - A landing page template for a B2C AI SaaS app, featuring carousel examples and product tours.](https://github.com/user-attachments/assets/a20b5c40-1955-48c4-b5f0-b8e3f47d3e9f)](https://shipixen.com/demo/landing-page-templates/template/gnomie-ai)
[![Minimum Via - A landing page template for a minimalistic product, or productized agency. Uses text and minimal colors to create a clean look.](https://github.com/user-attachments/assets/b654b414-d1c8-492f-92c6-9c798e28a207)](https://shipixen.com/demo/landing-page-templates/template/minimum-via)
[![ScreenshotTwo - A landing page template for a developer tool, featuring inline testimonials and a two-column layout with screenshots.](https://github.com/user-attachments/assets/6a778633-14de-455c-b5bf-8163929057ff)](https://shipixen.com/demo/landing-page-templates/template/screenshot-two)

[See all templates 👀](https://shipixen.com/demo/landing-page-templates) <br/>

## 💻 Installation (Next.js)

1️⃣ Start by creating a new Next.js app. You can use the following command:

```bash
npx create-next-app@latest my-app --typescript --tailwind --eslint
```

2️⃣ Run the Page UI CLI

```bash
npx @page-ui/wizard@latest init
```

3️⃣ Add the required dependencies to your Next.js app:

```bash
npm install @tailwindcss/forms @tailwindcss/typography tailwindcss-animate class-variance-authority clsx tailwind-merge lucide-react @radix-ui/react-accordion
```

4️⃣ Add the below to your `global.css` file.

<details>
<summary><b>Show code ↕️</b></summary>

```css
@layer base {
  :root {
    --hard-shadow: 0px 29px 52px 0px rgba(0, 0, 0, 0.4),
      22px 25px 16px 0px rgba(0, 0, 0, 0.2);
    --hard-shadow-left: 0px 29px 52px 0px rgba(0, 0, 0, 0.4),
      -22px 25px 16px 0px rgba(0, 0, 0, 0.2);
    /* If you use Shadcn UI already, you should already have these variables defined */
    --background: 0 0% 100%;
    --foreground: 240 10% 3.9%;
    --card: 0 0% 100%;
    --card-foreground: 240 10% 3.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 240 10% 3.9%;
    --primary-foreground: 355.7 100% 97.3%;
    --secondary: 240 4.8% 95.9%;
    --secondary-foreground: 240 5.9% 10%;
    --muted: 240 4.8% 95.9%;
    --muted-foreground: 240 3.8% 46.1%;
    --accent: 240 4.8% 95.9%;
    --accent-foreground: 240 5.9% 10%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 0 0% 98%;
    --border: 240 5.9% 90%;
    --input: 240 5.9% 90%;
    --radius: 0.5rem;
  }

  .dark {
    /* If you use Shadcn UI already, you can skip this block. */
    --background: 20 14.3% 4.1%;
    --foreground: 0 0% 95%;
    --card: 24 9.8% 10%;
    --card-foreground: 0 0% 95%;
    --popover: 0 0% 9%;
    --popover-foreground: 0 0% 95%;
    --primary-foreground: 144.9 80.4% 10%;
    --secondary: 240 3.7% 15.9%;
    --secondary-foreground: 0 0% 98%;
    --muted: 0 0% 15%;
    --muted-foreground: 240 5% 64.9%;
    --accent: 12 6.5% 15.1%;
    --accent-foreground: 0 0% 98%;
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 0 85.7% 97.3%;
    --border: 240 3.7% 15.9%;
    --input: 240 3.7% 15.9%;
  }

  *,
  ::before,
  ::after {
    @apply border-gray-100 dark:border-neutral-800;
  }

  * {
    @apply font-sans;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    @apply font-semibold font-display;
  }
}

@layer utilities {
  .text-balance {
    text-wrap: balance;
  }

  /**
   * Perspective (used for images etc.)
   */
  .perspective-none {
    transform: none;
  }

  .perspective-left {
    box-shadow: var(--hard-shadow);
    transform: perspective(400em) rotateY(-15deg) rotateX(6deg)
      skew(-8deg, 4deg) translate3d(-4%, -2%, 0) scale(0.8);
  }

  .perspective-right {
    box-shadow: var(--hard-shadow-left);
    transform: perspective(400em) rotateY(15deg) rotateX(6deg) skew(8deg, -4deg)
      translate3d(4%, -2%, 0) scale(0.8);
  }

  .perspective-bottom {
    box-shadow: var(--hard-shadow);
    transform: translateY(-4%) perspective(400em) rotateX(18deg) scale(0.9);
  }

  .perspective-bottom-lg {
    box-shadow: var(--hard-shadow);
    transform: perspective(400em) translate3d(0, -6%, 0) rotateX(34deg)
      scale(0.8);
  }

  .perspective-paper {
    box-shadow: var(--hard-shadow);
    transform: rotateX(40deg) rotate(40deg) scale(0.8);
  }

  .perspective-paper-left {
    box-shadow: var(--hard-shadow-left);
    transform: rotateX(40deg) rotate(-40deg) scale(0.8);
  }

  /**
   * Custom shadows
   */
  .hard-shadow {
    box-shadow: var(--hard-shadow);
  }

  .hard-shadow-left {
    box-shadow: var(--hard-shadow-left);
  }

  /**
   * Container utilities
   */
  .container-narrow {
    @apply max-w-4xl;
  }

  .container-wide {
    @apply xl:max-w-6xl;
  }

  .container-ultrawide {
    @apply xl:max-w-7xl;
  }
}
```

</details>

<br/>

For other frameworks, check out the [installation guide](https://pageui.dev/docs/installation).

> ✨ Skip the setup by bootstrapping your app with [Shipixen](https://shipixen.com).

## 🎨 Templates
To copy and paste from the available templates, visit [landing page templates](https://shipixen.com/demo/landing-page-templates).

## 💿 Demos
To see the components in action, visit [landing page component examples](https://shipixen.com/demo/landing-page-component-examples).

## 💪 Motivation

Designing and building landing pages that look good and convert well is hard business.<br/>
Most UI libraries focus on application UI, so when you set up a starer or boilerplate you end up staring at a blank canvas.<br/>
The time spent browsing through bloated templates, figuring out how to port them to your app and then customizing them is time you could spend on your product.

> Start from a blank canvas to create, start from Page UI to innovate.

## 📝 License
Licensed under the [MIT license](https://github.com/danmindru/page-ui/blob/main/LICENSE.md)

-----------------

Save 100s of hours of work by using Page AI to generate a beautiful website. In just minutes!

| | |
| :- | :- |
| <a href="https://pageai.pro" target="_blank"><img height="60px" src="https://pageai.pro/static/images/logo-square.png" alt="Page AI Logo" /></a> <br/> <b>Page AI</b> <br/> AI Website Generator that designs and writes clean code. <br/><br/> Try the app on <a href="https://pageai.pro">pageai.pro</a>. | <a href="https://pageai.pro" target="_blank"><img width="300px" src="https://user-images.githubusercontent.com/1515742/281077548-57b24773-3c2a-4e89-b088-cc3945d7037b.png" alt="Page AI Logo" /></a> |

-----------------

Apihustle is a collection of tools to test, improve and get to know your API inside and out. <br/>
[apihustle.com](https://apihustle.com) <br/>

|                                                                                                                                                                                        |              |                                                          |                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------- | :------------------------------------------------------- | :------------------------------------------- |
| <a href="https://pageai.pro" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/9bfbfe6f-add9-45de-aaf2-5c6043a47e41" alt="Page AI Logo" /></a>        | **Page AI**  | AI Website Generator that designs and writes clean code. | [pageai.pro](https://pageai.pro)             |
| <a href="https://shipixen.com" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/e1deba72-328e-4d3c-9c62-11ab77184561" alt="Shipixen Logo" /></a>     | **Shipixen** | Create a personalized blog & landing page in minutes     | [shipixen.com](https://shipixen.com)         |
| <a href="https://pageui.dev" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/b8815b62-598a-4fca-bc27-c03e66c8b105" alt="Page UI Logo" /></a>        | **Page UI**  | Landing page UI components for React & Next.js           | [pageui.dev](https://pageui.dev)             |
| <a href="https://clobbr.app" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/cb3e64e2-efaa-436b-ae6d-0ea4b47e4004" alt="Clobbr Logo" /></a>         | **Clobbr**   | Load test your API endpoints.                            | [clobbr.app](https://clobbr.app)             |
| <a href="https://crontap.com" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/38a3d734-d1ca-4f92-9cfb-ada52b9f2ffb" alt="Crontap Logo" /></a>       | **Crontap**  | Schedule API calls using cron syntax.                    | [crontap.com](https://crontap.com)           |
| <a href="https://tool.crontap.com" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/545f7618-ff2c-47fa-ad17-e17e38155f55" alt="CronTool Logo" /></a> | **CronTool** | Debug multiple cron expressions on a calendar.           | [tool.crontap.com](https://tool.crontap.com) |

-----------------

<a href="https://apihustle.com" target="_blank">
  <img height="60px" src="https://user-images.githubusercontent.com/1515742/215217833-c07183d2-f688-4d1c-86ea-329f3b28f81c.svg" alt="Apihustle Logo" />
</a>

-----------------

<img height="60px" src="https://github.com/danmindru/page-ui/assets/1515742/30259ef0-6085-401d-ab24-e9d1f9b5fc05" alt="Page UI logo" /> <br/>
Page UI ❤️ Open Source

