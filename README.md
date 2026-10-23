# Heirloom

**Record stories and messages for the people you love most.**

Heirloom is a parent-facing Progressive Web App for creating voice and video messages, stories, and letters for your children — sealed with a time-lock and gifted at the right moment. A message recorded today can be set to open when your child starts university, turns 18, or gets married. Heirloom keeps it safe until then.

---

## What it does

- **Record** — Capture video or audio directly in the browser. Choose from 40 curated prompts across five categories (Family stories, Milestones, Advice & letters, Us together, Just because), or record freely.
- **Seal** — Set a time-lock by date or life milestone. The recording stays locked until the moment arrives.
- **Gift** — When a recording unlocks, export it as a `.heirloom` file and share it via AirDrop, Messages, or email. Your child opens it in the Wide Eyes app.
- **Multiple contributors** — Each parent, grandparent, or family member has their own PIN-protected account on the same device.
- **Multiple children** — Recordings are linked to individual children and filtered per child.

---

## Design

The app uses a warm editorial aesthetic — DM Serif Display for headings, DM Sans for body text, a parchment ground, and gold accents. The home screen features a full-bleed photo background that starts as warm gradient placeholders and gradually replaces itself with photos from the user's own recordings.

---

## Tech

- Vanilla HTML, CSS, and JavaScript — no framework, no build step
- All data stored locally in IndexedDB (no cloud sync in Phase 1)
- MediaRecorder API for video and audio capture
- Progressive Web App — installable, works offline via service worker
- `.heirloom` export format: a JSON file containing the full entry including media and photos

---

## Getting started

### Run the build prompt

Heirloom is built from a single Claude Code prompt. Open a new Claude Code session in the directory where you want the project to live (e.g. alongside `wide-eyes-pwa/`), then paste the contents of `heirloom-build-prompt.md`.

Claude Code will scaffold the full `heirloom-pwa/` directory.

### Preview locally

```bash
cd heirloom-pwa
npx serve .
```

Then open `http://localhost:3000` in your browser. On first launch you'll be taken through onboarding to add a child and create your contributor account.

### Install as a PWA

In Chrome or Safari, use **Add to Home Screen** / **Install app** from the browser menu. Heirloom will open in standalone mode with no browser chrome.

---

## Project structure

```
heirloom-pwa/
  index.html        — app shell and screen templates
  app.js            — all application logic, routing, IndexedDB, MediaRecorder
  styles.css        — design system tokens, layout, components
  manifest.json     — PWA manifest
  sw.js             — service worker (cache-first, offline support)
  icons/
    icon-192.png
    icon-512.png
```

---

## Roadmap

| Phase | Status | Description |
|-------|--------|-------------|
| 1 — Local + file share | ✅ Current | Record, seal, and gift as `.heirloom` files. Multi-contributor, multi-child. |
| 2 — Local WiFi sync | Planned | Peer-to-peer sync between family members' devices on the same network. |
| 3 — Optional cloud | Planned | Encrypted cloud backup and sync across devices for families who want it. |

---

## Part of the Wide Eyes family

Heirloom is a companion to **Wide Eyes**, a journaling app for children. Wide Eyes receives and plays `.heirloom` files, letting children open their gifted recordings at the right moment.

---

*For the stories worth keeping.*# Heirloom
Parent version of Wide-Eyes
