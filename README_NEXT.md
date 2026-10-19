# Next Steps for Handoff

You have the recovered source at: ~/Desktop/erinleighton-replica/

## Recommended: Move everything to Erin (cleanest, no contact later)

1. **Create a repo** (GitHub/GitLab) under Erin's account, push this folder.
2. **Cloudflare**: Erin creates her own account, creates KV namespace SITE_DATA, adds the zone erinleighton.com there.
3. **Workers**: Erin deploys the worker.js (npx wrangler login/deploy) — update KV binding id in wrangler.toml to her namespace.
4. **Secrets**: Erin sets ADMIN_PASSWORD (`npx wrangler secret put ADMIN_PASSWORD`). The current admin password is the secret value that exists on the live worker; you'll need to share it (if you want her to access the admin) or she sets a new one.
5. **Domain**: At IONOS, remove transfer lock, get auth code; transfer domain to her or change nameservers to her Cloudflare.
6. **Cut ties**: Remove zone/worker from your Cloudflare account.

Alternatively, if you don't want to split Cloudflare: move erinleighton.com zone + KV to Erin's account (Cloudflare supports zone transfers between accounts in many cases), but Workers are account-scoped and harder to transfer.

## Quick verification
The site is ALREADY live at https://erinleighton.com with the current worker. It's working.

The API endpoints that exist:
- GET/POST /api/showreels (backed by KV)
- /api/login, /api/logout (admin auth)
- Others fallback to HTML

If you want, I can:
- Push this repo to GitHub (you need to auth)
- Generate the exact handoff checklist for IONOS/Cloudflare
- Tell you how to export/transfer the KV data (showreels content) to Erin's account
