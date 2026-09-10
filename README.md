# Analitica FULL

The current, full-featured analytics dashboard (dark ground; Day/Month/Year views, Difference
card, Top Expense card, Top‑5 Categories with "Дивитись усі", radial + bar charts, category detail
screens, cards & envelopes) packaged as a static Vite project for Vercel. This is the only
version in the project — the earlier light-theme screen has been retired.

## How it runs

- `index.html` boots a small runtime (`public/support.js`) that renders the whole app from the
  template + logic embedded in its `<x-dc>` / `<script data-dc-script>` blocks. The screen is
  fully self-contained (no sub-component fetches).
- `support.js` loads React/ReactDOM from a CDN (pinned SRI hash) at runtime if not already present.
- All local assets (category icons, the variable font, card/envelope art) are static files under
  `public/`, referenced by root-relative paths.

There is no separate `src/` app source to compile — Vite's only job is to serve/build this static
site.

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

Minimal, valid root-only skeleton — running `npm install` once resolves and rewrites it correctly.
