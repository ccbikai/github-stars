---
project: unlazy
stars: 769
description: 🪧 Universal lazy loading library for placeholder images leveraging native browser APIs
url: https://github.com/johannschopplich/unlazy
---

unlazy
======

Universal lazy loading library leveraging native browser APIs. It is intended to be used with the `loading="lazy"` attribute alongside (blurry) placeholder images and with a BlurHash or ThumbHash string.

Features
--------

-   🎀 **Native**: Utilizes the `loading="lazy"` attribute
-   🎛️ **Framework-agnostic**: Works with any framework or no framework at all
-   🌊 **BlurHash & ThumbHash support**: SSR & client-side BlurHash and ThumbHash decoding
-   🪄 **Sizing**: Automatically calculates the `sizes` attribute
-   🔍 **SEO-friendly**: Detects search engine bots and preloads all images
-   🎟 **`<picture>`**: Supports multiple image tags
-   🏎 **Auto-initialize**: Usable without a build step

Setup
-----

> 📖 Read the documentation

# pnpm
pnpm add -D unlazy

# npm
npm i -D unlazy

Basic Usage
-----------

> 📖 Read the documentation

To apply lazy loading to all images with the `loading="lazy"` attribute, import the `lazyLoad` function and call it without any arguments:

import { lazyLoad } from 'unlazy'

// Apply lazy loading for all images by the selector \`img\[loading="lazy"\]\`
lazyLoad()

You can target specific images by passing a CSS selector, a DOM element, a list of DOM elements, or an array of DOM elements to lazy-load to `lazyLoad`.

💻 Development
--------------

1.  Clone this repository
2.  Enable Corepack using `corepack enable`
3.  Install dependencies using `pnpm install`
4.  Run `pnpm run dev:prepare`
5.  Start development server using `pnpm run dev` inside the one of the `packages` directories

License
-------

MIT License © 2023-PRESENT Johann Schopplich
