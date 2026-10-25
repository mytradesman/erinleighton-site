# erinleighton-site

Source for **erinleighton.com** — a single-page portfolio served by a Cloudflare Worker.

## What to edit

All website content lives in **`worker.js`**.

Near the top you'll find:

```js
var HTML = `<!DOCTYPE html>
```

The entire page HTML is inside that backtick template literal. Edit only the HTML
inside those backticks. Keep every backtick, quote, and `${...}` expression intact —
breaking them breaks the site.

Do **not** edit `index.html`; it is only a reference copy.

## Deploy

Deployment is handled by the site owner:

```sh
npx wrangler deploy
```

The admin login (`/admin`) uses the `ADMIN_PASSWORD` Worker secret, which is not
stored in this repository. Set it before deploying if it is not already configured:

```sh
npx wrangler secret put ADMIN_PASSWORD
```
