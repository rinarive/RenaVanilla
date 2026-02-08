# Copilot / AI Agent Instructions for RenaVanilla

This repository is a small static portfolio site served from Firebase Hosting. The goal of an AI agent working here is to make focused, minimal edits to the front-end (HTML/CSS/JS), fix obvious path or asset issues, and prepare the site for local preview or Firebase deployment.

Key facts (actionable):

- **Project type:** Static site. Primary site root: `public/`.
- **Entry point:** `public/index.html` — edit UI/markup here.
- **Styles:** `public/style.css`.
- **JS:** There is `public/src/app.js` (currently empty). Note: `index.html` loads `app.js` from the site root (`<script type="module" src="app.js"></script>`). Verify script path — either move or update the reference to `src/app.js`.
- **Assets:** `public/iconos/` contains icons and images used by the site.
- **Hosting:** Firebase Hosting configured in `firebase.json`. Default project in `.firebaserc` is `renarivero-dev`.
- **Dependencies:** `package.json` lists `bulma` and `hover.css` (CSS libs). Most external libs are loaded via CDN in `index.html`.

Developer workflows (how to preview, test, and deploy):

- Local quick preview (no build tools required):

  - Option A (simple static server):

    - `npx http-server public` — serves the `public` folder on a local port.

  - Option B (Firebase CLI, recommended if installed):

    - Install CLI if needed: `npm install -g firebase-tools`.
    - Serve locally: `firebase serve --only hosting` or `firebase emulators:start --only hosting`.
    - Deploy: `firebase deploy --only hosting` (ensure authenticated & correct project).

- Install node deps (not strictly required for runtime): `npm install` (installs `bulma` and `hover.css` if you want local copies).

Project-specific conventions and gotchas (do these first):

- Static-only: There is no build tool or test runner. Avoid introducing tooling unless requested.
- Script path mismatch: `index.html` references `app.js` at site root but the JS file lives at `public/src/app.js`. Before adding logic, pick one approach and be consistent: either move `src/app.js` to `public/app.js` or change the script tag to `src/app.js`.
- CDN-first: Many libraries (Bootstrap, Bulma, FontAwesome) are referenced via CDN. Prefer keeping CDN usage unless asked to vendor the libs into `node_modules` and update links.
- Asset links are relative to `public/`. When modifying paths, check `public/index.html` and `firebase.json` rewrites (all routes rewrite to `/index.html`).

Where to make common changes:

- Layout / content edits: `public/index.html`.
- Styling: `public/style.css`.
- JavaScript logic: `public/src/app.js` (or `public/app.js` if you reconcile the path).
- Icons/images: `public/iconos/`.

Examples of useful edits an AI agent might be asked to perform:

- Fix the script path: update the `<script>` tag in `public/index.html` to `src/app.js` or move the file to `public/app.js`.
- Add small interactive behavior (e.g., smooth-scrolling helper or small DOM toggles) to the JS file; keep code minimal and use ES modules if `type="module"` is needed.
- Optimize images under `public/iconos/` (lossless compression) and update references if filenames change.

What NOT to do (unless explicitly requested):

- Do not add a full frontend build pipeline (Webpack/Vite) without user approval.
- Do not change hosting configuration (`firebase.json`) unless fixing a deployment issue.

References (files to inspect when doing work):

- `public/index.html`
- `public/style.css`
- `public/src/app.js`
- `public/iconos/`
- `firebase.json`
- `package.json`

If anything in these instructions is unclear or you'd like more detail (for example, a preferred local preview command, or whether to vendor CSS libs), tell me which section to expand and I'll update this file.
