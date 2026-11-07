# Deploy Akraya Chat

This guide deploys the backend Worker and static frontend to your own Cloudflare account.

## Requirements

- A Cloudflare account with Workers AI enabled
- Node.js and `npx`
- Wrangler (the `npx wrangler` commands below can run it without a global install)

## 1. Sign in

```sh
npx wrangler login
npx wrangler whoami
```

## 2. Deploy the Worker

```sh
cd backend
npx wrangler deploy
```

Record the deployed Worker URL, usually `https://chat-api.<your-subdomain>.workers.dev`.

## 3. Set the frontend API endpoint

In `frontend/index.html`, find the **DEPLOY CONFIG** block. In the supplied version, `API_BASE_URL` is currently around line 1110. Set the fallback URL to the Worker URL from step 2:

```js
const API_BASE_URL = window.CHAT_API_BASE || 'https://chat-api.<your-subdomain>.workers.dev';
```

You can alternatively set `window.CHAT_API_BASE` before the app script runs. Do not leave the placeholder URL in place.

## 4. Deploy the frontend

From the repository root:

```sh
npx wrangler pages project create chat-web --production-branch main
npx wrangler pages deploy frontend --project-name chat-web
```

If you already created the Pages project, skip the `project create` command and deploy directly.

## 5. Check the deployment

Open your Pages URL and send a short test message. The Worker API route is `/simplechat` and accepts `userId` and `message` query parameters. Review the Cloudflare dashboard for errors and usage after the request.

## Before sharing your deployment

The frontend includes a music track credited in its original project materials to Pixabay. Confirm that your redistribution and use comply with the track's license. Set up privacy information and service terms that accurately describe your own deployment. AI responses can be inaccurate; users and operators should verify important information and not treat responses as professional or emergency advice.
