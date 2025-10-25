---
project: lmrouter
stars: 241
description: |-
    An open-source, all-in-one AI API router
url: https://github.com/LMRouter/lmrouter
---

# LMRouter

**LMRouter** is an open-source, all-in-one API router that gives AI developers a single, unified way to connect to the best model providers.

With LMRouter, you don’t need to create accounts on multiple platforms or juggle different API keys. A **single API key** unlocks access to **any provider, any model, any service**, all through one interface.

It’s an **open-source alternative to OpenRouter**, but goes far beyond language models. LMRouter supports multiple modalities and services out of the box:

- **Language**: Chat Completions, Responses API, Anthropic Messages
- **Image**: Image generation and editing
- **Audio**: Speech-to-text and audio models
- **Video**: Video generation (coming soon)
- **Embeddings**: Semantic search and RAG
- **Search**: Jina, Exa, and other web search APIs (coming soon)
- **Code**: Execution with interpreters such as e2b (coming soon)

## Quick Start

LMRouter service is available at [lmrouter.com](https://lmrouter.com). Please refer to the [documentation](https://docs.lmrouter.com/) for more information.

### Local Development/Deployment

To setup LMRouter locally, make sure you have Node.js and [pnpm](https://pnpm.io/installation) installed, then follow these steps:

```bash
git clone https://github.com/LMRouter/lmrouter
cd lmrouter
pnpm i
cp config/config.example.yaml config/config.yaml
```

Edit `config/config.yaml` to set up your own provider and model configurations.

```bash
# Run the server in development mode
pnpm dev

# Run the server in production mode
pnpm build
pnpm start
```

Alternatively, you can use `pnpx` to run the server:

```bash
pnpx @lmrouter/cli /path/to/config.yaml
```

## Features

### API Compatibility

LMRouter provides drop-in compatibility with existing APIs, so applications that already work with OpenAI or Anthropic can integrate without changes:

```
OpenAI API
  /openai/v1/chat/completions     — Chat Completions
  /openai/v1/images/generations   — Image generation
  /openai/v1/images/edits         — Image editing
  /openai/v1/embeddings           — Embeddings
  /openai/v1/responses            — Responses
  /openai/v1/audio/speech         — Audio speech
  /openai/v1/audio/transcriptions — Audio transcriptions
  /openai/v1/audio/translations   — Audio translations
  /openai/v1/models               — List available models

Anthropic API
  /anthropic/v1/messages          — Messages
  /anthropic/v1/models            — List available models
```

### Multi-Provider Support

LMRouter connects to the broader AI ecosystem, with built-in support for:

- **OpenAI-compatible** — OpenAI, Google, Perplexity, Fireworks, Groq, Cerebras, etc.
- **Anthropic-compatible** — Anthropic, Amazon Bedrock, etc.
- **Fireworks** — FLUX.1 [schnell] FP8, FLUX.1 Kontext Pro, FLUX.1 Kontext Max
- **Google** — Imagen, Gemini image generation, etc.

### Multi-Runtime Deployment

LMRouter is built on [Hono](https://hono.dev/) and runs in multiple environments:

- **Node.js** — Standard server deployment
- **Cloudflare Workers** — Lightweight edge deployment at scale

## Contributing

We believe LMRouter should be built **by the community, for the community**. Every contribution, whether it’s fixing a bug, adding a feature, improving documentation, or sharing feedback, helps make LMRouter stronger.

### Roadmap

Checkout our [Kanban](https://github.com/orgs/LMRouter/projects/1) for the latest roadmap.

### How to Get Started

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/my-feature`)
3. **Build** your changes, code, docs, or tests
4. **Verify** everything works as expected
5. **Submit** a pull request and join the conversation

No contribution is too small, even a typo fix helps. And if you have big ideas, we’d love to hear them.

> **Tip:** If you’re not sure where to start, check out the open issues labeled `good first issue`.

## License

LMRouter is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

