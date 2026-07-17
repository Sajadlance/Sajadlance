<!-- markdownlint-disable MD013 MD033 MD041 -->

<div align="center">
  <a href="https://hiprax.com"><img alt="Sajad Khanmirzaei: Full-Stack Developer, DevOps Engineer and Applied AI. Open to opportunities." src="assets/banner.svg" width="100%" /></a>
</div>

<h1 align="center">Sajad Khanmirzaei</h1>

<p align="center">
  Full-Stack Developer&nbsp; ·&nbsp; DevOps Engineer&nbsp; ·&nbsp; Applied AI&nbsp; ·&nbsp; Founder &amp; CEO of <a href="https://hiprax.com">Hiprax</a>
</p>

<p align="center">
  <a href="https://hiprax.com"><img alt="Website" height="28" src="https://img.shields.io/badge/hiprax.com-6366F1?style=for-the-badge&logo=googlechrome&logoColor=white" /></a>
  <a href="https://www.npmjs.com/~hiprax"><img alt="npm packages" height="28" src="https://img.shields.io/badge/npm-CB3837?style=for-the-badge&logo=npm&logoColor=white" /></a>
  <a href="https://linkedin.com/in/sajadkhmz"><img alt="LinkedIn" height="28" src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" /></a>
  <a href="mailto:sajad@hiprax.com"><img alt="Email" height="28" src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" /></a>
</p>

<div align="center">
  <img alt="Divider" src="assets/divider.svg" width="100%" />
</div>

## ~/about

I build web applications end to end, and then I keep them alive.

That second half is where it gets interesting. Shipping a demo is easy. Surviving real traffic, a bored attacker, and a bad deploy on a Friday afternoon is a different job, and it's the one I actually like. I founded **[Hiprax](https://hiprax.com)** to do that work with two engineers I've known for years.

Most of my time now goes to the seam between production engineering and applied AI: retrieval pipelines, agents that take real actions, voice interfaces, and the deeply unglamorous plumbing that keeps them predictable on the days a model decides to get creative.

Ten years and sixty-odd projects in, every client has come back for more. That's the metric I care about.

## ~/how-i-ship

<div align="center">
  <img alt="The architecture I ship on: a client request travels through Cloudflare to Nginx on the host, which terminates TLS and proxies to a single port bound to 127.0.0.1. Inside the Docker Compose boundary an internal Nginx routes to the app, which reads and writes MongoDB and enqueues jobs on Redis for a worker to consume." src="assets/architecture.svg" width="100%" />
</div>

Every project I take on gets deployed the same shape. One compose file, one root `.env`, one port on the loopback interface, and an Nginx on the host holding the only certificate. There is exactly one door into the stack, and everything else talks over the compose network where the internet can't reach it.

Here's the detail that decides it. Publish a container port without binding it to `127.0.0.1` and Docker DNATs it in the `nat` table before your firewall ever gets a say. The packet is routed through `FORWARD`, where Docker's own rules accept it, and never reaches the `INPUT` chain where your `ufw` rules live. So the port you believe is closed is open to the whole internet, and `ufw status` will happily tell you it's blocked. Plenty of "firewalled" stacks are wide open for exactly this reason.

None of this is clever, and that's the point. I can rebuild it on a bare VPS in an afternoon, and so can whoever inherits it from me.

## ~/work

Products I've built with Hiprax. Most are under NDA, so these are the shapes rather than the client names.

| Project | What it does | Stack |
| :-- | :-- | :-- |
| **AI Print-on-Demand Studio** | Generate original artwork from a prompt, refine it in a full in-browser design editor, then order it on real products. | MERN · Fabric.js · Socket.io · GenAI |
| **AI Political Transparency** | Aggregates political news and fact-checks live speech in real time, with a conversational AI for civic questions. | MERN · WebSocket / SSE · AI |
| **Omnichannel AI Sales** | A subscription CRM where businesses train custom AI agents that run SMS and voice outreach and close deals on their own. | MERN · Stripe · AI |
| **Conversational AI Ordering** | Human-like voice AI that answers restaurant calls and takes orders through natural conversation. | Python · TensorFlow · Transformers · FastAPI |
| **Financial Fraud Prevention** | Real-time verification so people can tell a genuine bank contact from an impersonation scam. | Node · React · REST |
| **Stereoscopic 3D Streaming** | Dual-camera live pipeline with intelligent object alignment for real-time stereoscopic display. | Computer Vision · Streaming |

<details>
<summary><b>The full list — the 23 I can name</b></summary>

AI Company Showcase & Marketing Website · AI Market Intelligence Suite · AI Print-on-Demand Design Studio · AI-Powered Investment Signal Platform · AI-Powered Political Transparency Platform · Advanced HTTP Parameter Pollution Shield · Conversational AI Ordering System · Dynamic Audio Visualization Engine · Enterprise Admin Dashboard UI Kit · Enterprise-Grade Encryption Library · Financial Fraud Prevention Platform · Full-Stack Image Processing & Delivery System · Full-Stack Ticketing & Support Management System · Government Document Automation Suite · Omnichannel AI Sales Engagement Platform · Peer-to-Peer Storage Marketplace · Production-Grade Structured Logging Toolkit for Node.js · React SEO Management Hook · Real Estate Auction Intelligence System · Real-Time Penny Auction Platform · Social Engagement Rewards Platform · Stereoscopic 3D Streaming System · Vending Machine Operations Platform

Five of them are open source; you can read every line in the next section. The rest live at **[hiprax.com](https://hiprax.com/#projects)**.

</details>

## ~/open-source

Seven packages on **[npm](https://www.npmjs.com/~hiprax)** — four under the `@hiprax` scope, three unscoped — all MIT. Around 11,600 downloads in the last year: modest, real, and not a vanity number. `@hiprax/crypto` and `@hiprax/logger` publish from CI through npm's OIDC trusted publishing, so no token ever touches a laptop.

| Package | What it gives you |
| :-- | :-- |
| **[`@hiprax/crypto`](https://www.npmjs.com/package/@hiprax/crypto)** <br> [![npm version](https://img.shields.io/npm/v/@hiprax/crypto?style=flat-square&labelColor=0a0a0a&color=6366f1&logo=npm&logoColor=white)](https://www.npmjs.com/package/@hiprax/crypto) [![downloads per year](https://img.shields.io/npm/dy/@hiprax/crypto?style=flat-square&labelColor=0a0a0a&color=22d3ee)](https://www.npmjs.com/package/@hiprax/crypto) [![source](https://img.shields.io/badge/source-0a0a0a?style=flat-square&logo=github&logoColor=white)](https://github.com/Hiprax/crypto) | AES-256-GCM authenticated encryption with Argon2id key derivation, file streaming, and constant-time comparison. Zero runtime dependencies. |
| **[`hppx`](https://www.npmjs.com/package/hppx)** <br> [![npm version](https://img.shields.io/npm/v/hppx?style=flat-square&labelColor=0a0a0a&color=6366f1&logo=npm&logoColor=white)](https://www.npmjs.com/package/hppx) [![downloads per year](https://img.shields.io/npm/dy/hppx?style=flat-square&labelColor=0a0a0a&color=22d3ee)](https://www.npmjs.com/package/hppx) [![source](https://img.shields.io/badge/source-0a0a0a?style=flat-square&logo=github&logoColor=white)](https://github.com/Hiprax/hppx) | HTTP Parameter Pollution shield for Express: blocks prototype pollution, null-byte injection, and DoS vectors with nested whitelists. |
| **[`pixel-serve-server`](https://www.npmjs.com/package/pixel-serve-server)** <br> [![npm version](https://img.shields.io/npm/v/pixel-serve-server?style=flat-square&labelColor=0a0a0a&color=6366f1&logo=npm&logoColor=white)](https://www.npmjs.com/package/pixel-serve-server) [![downloads per year](https://img.shields.io/npm/dy/pixel-serve-server?style=flat-square&labelColor=0a0a0a&color=22d3ee)](https://www.npmjs.com/package/pixel-serve-server) [![source](https://img.shields.io/badge/source-0a0a0a?style=flat-square&logo=github&logoColor=white)](https://github.com/Hiprax/pixel-serve-server) | Sharp-powered image middleware: on-the-fly AVIF and WebP conversion, resizing, strict path validation, smart caching. |
| **[`pixel-serve-client`](https://www.npmjs.com/package/pixel-serve-client)** <br> [![npm version](https://img.shields.io/npm/v/pixel-serve-client?style=flat-square&labelColor=0a0a0a&color=6366f1&logo=npm&logoColor=white)](https://www.npmjs.com/package/pixel-serve-client) [![downloads per year](https://img.shields.io/npm/dy/pixel-serve-client?style=flat-square&labelColor=0a0a0a&color=22d3ee)](https://www.npmjs.com/package/pixel-serve-client) [![source](https://img.shields.io/badge/source-0a0a0a?style=flat-square&logo=github&logoColor=white)](https://github.com/Hiprax/pixel-serve-client) | The React half of Pixel Serve: multi-format srcset, lazy loading, a skeleton loader, SSR-safe fallbacks. |
| **[`@hiprax/use-seo`](https://www.npmjs.com/package/@hiprax/use-seo)** <br> [![npm version](https://img.shields.io/npm/v/@hiprax/use-seo?style=flat-square&labelColor=0a0a0a&color=6366f1&logo=npm&logoColor=white)](https://www.npmjs.com/package/@hiprax/use-seo) [![downloads per year](https://img.shields.io/npm/dy/@hiprax/use-seo?style=flat-square&labelColor=0a0a0a&color=22d3ee)](https://www.npmjs.com/package/@hiprax/use-seo) [![source](https://img.shields.io/badge/source-0a0a0a?style=flat-square&logo=github&logoColor=white)](https://github.com/Hiprax/use-seo) | One React hook for titles, Open Graph, Twitter Cards, hreflang, and JSON-LD. SSR-safe and fully tested. |
| **[`@hiprax/logger`](https://www.npmjs.com/package/@hiprax/logger)** <br> [![npm version](https://img.shields.io/npm/v/@hiprax/logger?style=flat-square&labelColor=0a0a0a&color=6366f1&logo=npm&logoColor=white)](https://www.npmjs.com/package/@hiprax/logger) [![downloads per year](https://img.shields.io/npm/dy/@hiprax/logger?style=flat-square&labelColor=0a0a0a&color=22d3ee)](https://www.npmjs.com/package/@hiprax/logger) [![source](https://img.shields.io/badge/source-0a0a0a?style=flat-square&logo=github&logoColor=white)](https://github.com/Hiprax/logger) | Winston-based structured logging with daily rotation, verified IANA timezones, and an Express middleware that masks secrets automatically. |
| **[`@hiprax/errors`](https://www.npmjs.com/package/@hiprax/errors)** <br> [![npm version](https://img.shields.io/npm/v/@hiprax/errors?style=flat-square&labelColor=0a0a0a&color=6366f1&logo=npm&logoColor=white)](https://www.npmjs.com/package/@hiprax/errors) [![downloads per year](https://img.shields.io/npm/dy/@hiprax/errors?style=flat-square&labelColor=0a0a0a&color=22d3ee)](https://www.npmjs.com/package/@hiprax/errors) [![source](https://img.shields.io/badge/source-0a0a0a?style=flat-square&logo=github&logoColor=white)](https://github.com/Hiprax/errors) | Modular error handling for Express: structured, typed error classes and consistent API responses. |

## ~/stack

| Layer | Tools |
| :-- | :-- |
| **Frontend** | React · TypeScript · Next.js · Tailwind · Three.js |
| **Backend** | Node · Express · Python · FastAPI · Django |
| **Data** | MongoDB · Redis · PostgreSQL · MySQL · Elasticsearch |
| **Infra** | Linux · Docker · Kubernetes · Nginx · AWS · Cloudflare · GitHub Actions |
| **Applied AI** | RAG · agents · OpenAI · LangChain · Hugging Face · PyTorch · Whisper / voice |
| **Security** | OWASP · OAuth / JWT · AES-GCM · Argon2id · TLS · pentesting |

Vue, Svelte, Angular, Flask, PHP, and Laravel are in the toolbox too, when a project already lives there.

## ~/principles

> **No shortcuts. No hand-holding frameworks. No blind dependency on AI.** <br>
> Just engineers who understand what they build, top to bottom.
>
> I'd rather ship something I can debug at 3am than something I can only demo.

## ~/connect

Open to full-time roles, contracts, and the occasional interesting collaboration. I work remotely with teams anywhere.

The fastest way to reach me is email. Tell me what you're building, what it runs on, and what's currently on fire.

<p align="center">
  <a href="mailto:sajad@hiprax.com"><img alt="Email" height="28" src="https://img.shields.io/badge/sajad@hiprax.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white" /></a>
  <a href="https://linkedin.com/in/sajadkhmz"><img alt="LinkedIn" height="28" src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" /></a>
</p>

<div align="center">
  <img alt="Divider" src="assets/divider.svg" width="100%" />
  <br /><br />
  <sub>
    Three hand-written SVGs and a few live npm badges. No stats card, no streak counter, no snake.<br />
    Every animation is CSS and respects <code>prefers-reduced-motion</code>.<br />
    The stats card is missing on purpose: almost everything I build is under NDA in private repos, so it would only ever measure the sliver that isn't.
  </sub>
</div>
