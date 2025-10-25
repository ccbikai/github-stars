---
project: takumi
stars: 843
description: |-
    Render your React component to images. satori + resvg but with variable fonts, RTL, inline layout, WOFF2 support.
url: https://github.com/kane50613/takumi
---

<img src="./assets/images/takumi.svg" alt="Takumi" width="64" />

# Takumi

Takumi is an **image rendering engine** written in Rust that provides bindings for Node.js and WebAssembly. Suitable for high-throughput image rendering workloads such as Open Graph images and Twitter images.

For newcomers, you can try out Takumi in [playground](https://takumi.kane.tw/playground) without installation. Or check [Getting Started](https://takumi.kane.tw/docs/getting-started/) page for usage.

## Why build a satori alternative?

- All in one. No need to output SVG then have [resvg-js](https://github.com/thx/resvg-js) rendering it again to output PNG.
- Inline layout support (display `block` or `inline`).
- RTL support.
- Variable fonts support.
- WOFF2 font format support.
- PNG, JPEG, WebP, AVIF output support.
- WebP, APNG animation rendering support.

## Goals

- Takes your existing JSX components and drops them in, it should just work.
- Minimal binary size targets to run everywhere.
- Be the go-to library for image/animation rendering.
- Have a great developer experience.

## Showcase

- Takumi's Open Graph image is generated with Takumi [(source)](./example/twitter-images/components/og-image.tsx).

  ![Takumi OG Image](./example/twitter-images/output/og-image.png)

- X Post Image clone in embed [(source)](./example/twitter-images/components/x-post-image.tsx).

  ![X OG Image](./example/twitter-images/output/x-post-image.png)

- [shiki-image](https://github.com/pi0/shiki-image) Convert code snippets into images.

  ![Shiki Image Example](https://github.com/pi0/shiki-image/blob/main/test/.snapshot/image.webp)

- [(Unofficial) Takumi Playground](https://takumi-playground.kapadiya.net/) In-browser playground for designing and rendering Open Graph style images.

## License

Licensed under the terms in the [LICENSE](LICENSE) file.

