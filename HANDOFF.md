# erinleighton.com - Site source (recovered)

This folder contains the *actual* Worker source recovered from the live Cloudflare Worker (`erin-website`).

## Files
- `worker.js` — Full bundled Cloudflare Worker (HTML embedded + API + admin logic). Deployable as-is.
- `index.html` — Static copy of the homepage (for reference only).
- `wrangler.toml` — Wrangler config with KV binding for `SITE_DATA`.

## Architecture
- Served by Cloudflare Worker `erin-website` (bound to domain `erinleighton.com`)
- Has an admin system:
  - `/api/login` — password auth (ADMIN_PASSWORD stored as Worker secret)
  - `/api/logout`
  - `GET /api/showreels` — reads showreels from KV
  - `POST /api/showreels` — updates showreels (auth required)
- Showreels: if KV has showreels data, it's used; otherwise the HTML's hardcoded fallback is shown

## Deployment
```bash
npx wrangler login
npx wrangler deploy
```

Note: The deployed Worker has secrets/bindings. If deploying from a new account, you'll need to:
1. Create KV namespace `SITE_DATA` and update `wrangler.toml` with its ID
2. Set `ADMIN_PASSWORD` secret: `npx wrangler secret put ADMIN_PASSWORD`
3. Also handle any other secrets the worker may use

## Notes
- `index.html` is included for quick reference/editing. If you edit the HTML, you'll need to embed it back into `worker.js` (or refactor the worker). Since the worker currently serves the HTML from a template string, editing the HTML inside `worker.js` is the cleanest way.
- The API endpoints return JSON. The site currently has `/api/showreels` returning empty data (using fallback HTML content).