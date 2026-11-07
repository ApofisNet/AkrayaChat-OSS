# Akraya Chat

<p align="center">
  <img src="frontend/favicon.svg" width="88" alt="Akraya butterfly logo">
</p>

<p align="center"><strong>A quiet, open-source AI companion you can run on your own Cloudflare account.</strong></p>

<p align="center">
  <img src="https://img.shields.io/badge/Cloudflare-Workers%20AI-F38020?style=flat-square" alt="Cloudflare Workers AI">
  <img src="https://img.shields.io/badge/license-MIT-87D0EF?style=flat-square" alt="MIT License">
</p>

---

This repository contains Akraya Chat's static web interface and Cloudflare Worker. It is shared by **Apofis Group** for people who want to deploy and adapt the software on infrastructure they control.

The design takes its visual cues from Akraya's original About page: a warm parchment background, soft blue butterfly mark, and calm typography. The source app and About page are preserved as supplied.

## What it includes

- `frontend/` — static chat interface and assets
- `backend/` — Cloudflare Worker using the Workers AI binding
- [`Deploy.md`](Deploy.md) — deployment instructions for your Cloudflare account

## Deploy

Follow [`Deploy.md`](Deploy.md). You can use Claude Code or another AI coding assistant to walk through those steps; check each account action before confirming it.

### API endpoint to customize

The assistant must connect the frontend to the Worker you deploy. In `frontend/index.html`, find the **DEPLOY CONFIG** block. In this supplied version, the API endpoint setting is on **line 1137**:

```js
const API_BASE_URL = window.CHAT_API_BASE || 'https://apiv1.akraya.club';
```

For your deployment copy, change the fallback URL to your own Worker URL (for example, `https://chat-api.<your-subdomain>.workers.dev`). The same value can be supplied via `window.CHAT_API_BASE` before the app script runs. The source app file is preserved in this repository; the line number may shift if it changes.

## Endpoint locations

| Purpose | File and location |
|---|---|
| Frontend API origin | `frontend/index.html`, `DEPLOY CONFIG`, currently around line 1110 (`API_BASE_URL`) |
| Worker name and deployment settings | `backend/wrangler.toml`, `name` near line 3 |
| API route | `backend/src/worker.js`, request handler; `/simplechat?userId=…&message=…` |
| Cloudflare AI model | `backend/src/worker.js`, model declaration near line 6333 |

The Worker responds with a server-sent event stream. Its CORS policy currently allows all origins; restrict that for a public deployment if your setup requires it.

## AI output and responsibility

This project uses AI to generate responses. Operators and users are responsible for how they use those responses and should independently verify important information. AI responses may be inaccurate and are not a substitute for professional advice.

## Branding and service information

The frontend retains the Akraya logo, chat landing experience, and music control. It does not include the original hosted-service About page, privacy policy, or terms. Each operator should provide service information that accurately describes their deployment.

## License

This project is provided under the MIT License. You may use, modify, and redistribute it, including commercially. MIT requires preserving the copyright and license notice in copies or substantial portions of the software. See [LICENSE](LICENSE).

The license only covers rights Apofis Group can grant. Third-party assets and services remain subject to their own terms. The ambient audio is credited in `frontend/INFO.html` to Pixabay's Content License; verify its license and any relevant terms before redistributing it in your intended way. Cloudflare, model, font, and other external services are not relicensed by this repository.

## Company and project details to confirm

Before publishing, replace the copyright holder placeholder in `LICENSE` with the exact legal name of the rights-owning company and confirm the company has rights to all included code and assets. Check the duplicate `backend/original-bundle.txt` against the source-release plan; it contains a second full copy of the Worker.
