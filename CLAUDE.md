# Heirloom — CLAUDE.md

Heirloom is a parent-facing PWA (companion to Wide Eyes) for recording video/audio messages, sealing them with a time-lock, and gifting them as `.heirloom` files. The app lives in `heirloom-pwa/`. Read `heirloom-pwa/README.md` for the data model, `.heirloom` format, backups/restore and known limitations.

## Architecture

- Vanilla HTML/CSS/JS: `index.html`, `app.js`, `styles.css`, `sw.js`, `manifest.json`. No framework, no build step, no npm dependencies. JSZip is loaded from cdnjs only for backup/restore.
- All data on-device: IndexedDB `heirloom-db` (stores `heirloom-entries`, `heirloom-profiles`, `heirloom-bg`) plus a few small localStorage flags. No backend.
- Deployed by Cloudflare Pages (build output directory `heirloom-pwa`); pushing to `main` deploys to production. Heirloom must not share a URL with SunTimeKids.

## Coding rules

1. **No inline event handlers.** Wire with `addEventListener`. Every static element is wired exactly once, in `wireStatic()`. Dynamic lists use event delegation (`data-action`, `data-id`). Buttons created at runtime inside modals/sheets are wired where they are created. Wiring something twice makes it fire twice.
2. **No `innerHTML` with dynamic content.** Build DOM with `el(tag, props, children)` and `clearEl(node)`. Names, titles and prompts are user or library text and always go through `textContent`.
3. **Apostrophes**: a JS string containing an apostrophe uses double quotes or a template literal, never single quotes.
4. **Storage**: wrap every IndexedDB/localStorage call so failure shows a friendly on-screen message (`storageError`, `lsGet`/`lsSet`).
5. **Relative paths only** in `index.html`, `manifest.json` and `sw.js`, so the app works from any path.
6. **Service worker**: bump `CACHE` in `sw.js` whenever a shell file changes, or installed copies keep the old version.

## Before committing

```bash
node --check heirloom-pwa/app.js
node --check heirloom-pwa/sw.js
node -e "JSON.parse(require('fs').readFileSync('heirloom-pwa/manifest.json','utf8'))"
```

A syntax check does not catch logic bugs. Serve `heirloom-pwa/` locally and click through: onboarding → PIN → record → photos → seal → detail → unlock → share → settings (backup, restore). Headless Chromium can fake the camera and mic with `--use-fake-device-for-media-stream --use-fake-ui-for-media-stream`.

## Before launch

- Set `TESTING_MODE_DEFAULT` in `app.js` to `false` (it offers a backup after every recording while the app is being tested).
