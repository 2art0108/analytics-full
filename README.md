# Nocturne Analytics Prototype

A self-contained interactive HTML/JS prototype (dark analytics dashboard — Day/Month/Year views,
radial + bar charts, merchant/category breakdown) packaged as a static Vite project for Vercel.

## How it runs

- `index.html` boots a small runtime (`public/support.js`) that renders the whole app from the
  template + logic embedded in `index.html`'s `<x-dc>`/`<script data-dc-script>` blocks.
- `support.js` loads React/ReactDOM from a CDN (with a pinned SRI hash) at runtime if not already
  present — no React/JSX source or bundling step is required.
- All local assets (category icons, the variable font, merchant/category data) are static files
  under `public/uploads/` and `public/support.js`, referenced by root-absolute paths so they work
  identically in `vite dev`, `vite build`, and on Vercel.

There is no separate `src/` app source to compile — Vite's only job here is to serve/build this
static site (dev server, asset copying, `dist/` output) so it deploys the same way any other
Vite static project does.

## Local setup

```bash
npm install
npm run dev      # http://localhost:5173
npm run build    # outputs to dist/
npm run preview  # serve the dist/ build locally
```

## Deploy

```bash
git init && git add -A && git commit -m "Initial commit"
# push to a new GitHub repo, then import it in Vercel (Framework Preset: Vite)
```
`vercel.json` pins the build command and `dist` as the output directory.

## Note on package-lock.json

This lockfile is a minimal, valid root-only skeleton (no fabricated dependency/integrity entries).
This project was authored in a sandboxed design tool without live npm-registry access, so a
byte-accurate lockfile couldn't be generated here. Running `npm install` once will resolve
`vite`'s real dependency tree and rewrite this file completely and correctly — after that first
install it's a normal, accurate lockfile safe to commit.

## Verification performed here

- Confirmed every local asset the app references (icons, font, `support.js`) exists under
  `public/` at the exact path the app requests it from.
- Confirmed `index.html` has no build-time JS imports/bundling requirements — the one classic
  `<script src="/support.js">` and the `@font-face` reference both use root-absolute paths, which
  Vite/Vercel serve unmodified from `public/`.
- Could not execute `npm install` / `npm run build` directly (no Node/npm shell in this tool) —
  please run the Local setup commands above once after extracting to confirm the build end-to-end.
