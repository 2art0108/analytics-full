# Analitica FULL

A self-contained interactive HTML/JS prototype — a dark-ground and light-ground analytics
dashboard (Day/Month/Year views, radial + bar charts, merchant/category breakdown, cards &
envelopes) packaged as a static Vite project for Vercel.

## Pages

- `/` (`index.html`) — Analytics Screen (light theme)
- `/dark.html` — Analytics Screen (dark theme)

Both boot a small runtime (`public/support.js`) that renders the page from the template + logic
embedded in each file's `<x-dc>` / `<script data-dc-script>` blocks. The light screen loads its
status bar as a small sub-component (`public/StatusBar.dc.html`), fetched by the runtime at
`/StatusBar.dc.html`; `public/StatusBarDark.dc.html` ships alongside it for parity even though the
dark screen currently inlines its own status bar markup.

`support.js` loads React/ReactDOM from a CDN (pinned SRI hash) at runtime if not already present —
no React/JSX source or bundling step is required. All local assets (category icons, the variable
font, card/envelope art, background image) are static files under `public/`, referenced by
root-relative paths so they resolve identically in `vite dev`, `vite build`, and on Vercel.

There is no separate `src/` app source to compile — Vite's job here is to serve/build this static
multi-page site (dev server, asset copying, `dist/` output for both `index.html` and `dark.html`).

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

This lockfile is a minimal, valid root-only skeleton (no fabricated dependency/integrity entries) —
this project was authored without live npm-registry access. Running `npm install` once resolves
`vite`'s real dependency tree and rewrites this file completely and correctly; after that first
install it's a normal, accurate lockfile safe to commit.
