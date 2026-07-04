# Agent guide — voxel-box.github.io

Instructions for AI coding agents (and new contributors) working on this repository.

## The one-paragraph mental model

This is a **static GitHub Pages site with zero tooling**: no package.json, no build,
no framework. Each page is one self-contained `.html` file containing its own CSS and
vanilla JS. GitHub Pages serves the `main` branch at **https://voxel-box.github.io**,
so merging to `main` deploys. There is nothing to install and nothing to compile —
verify changes by opening the HTML file in a browser.

## Repository map

- `index.html` — Voxelbox homepage. Sections: hero, `#servers` (7 server cards with
  IPs), `#rules` (per-server rule cards), `#community`. Brand palette is defined in
  `:root` CSS variables (orange `#ff8a00` on dark greys).
- `hermes/index.html` — **Hermes OS**, a browser desktop hub. Structure inside the file:
  1. **Theme engine** (top of `<style>`): one `:root[data-theme="…"]` block per theme.
  2. **Data** (top of `<script>`): `SERVERS`, `RULES`, `THEMES` constants.
  3. **App registry**: the `APPS` object — each key is an app.
  4. **Window manager**: `openApp()`, dragging, z-order, taskbar chips.
- `voxelbox-org/` — versioned source of the live **https://voxelbox.org** site
  (captured 2026-07-04). 26 pages sharing `voxel.css`/`voxel.js`, plus a Three.js
  voxel-world scene (`voxel-world.js`, ES module — needs HTTP, not `file://`).
  NOTE: this directory is NOT auto-deployed to voxelbox.org — that domain is hosted
  elsewhere; edits here must be uploaded to its host. See `voxelbox-org/README.md`.
- `README.md` — human-facing overview.

## Hard rules

1. **Keep pages self-contained.** No CDNs, no external fonts/scripts/frameworks.
   Inline everything. This is deliberate — the site must work with zero dependencies.
2. **Keep server data in sync.** Server names/tags/rules exist in BOTH `index.html`
   (markup) and `hermes/index.html` (`SERVERS`/`RULES` constants). Change both.
   The canonical, most current server lineup is the one on voxelbox.org
   (`voxelbox-org/servers.html`).
3. **Never publish server addresses.** No IPs, ports, hostnames, or connection
   strings anywhere in this repo — join info lives in the Discord on purpose so it
   stays current and off the public record. Point people at
   https://discord.gg/mpeZ62uEEp instead.
4. **Don't commit secrets or chat logs.** This repo is public. Access tokens,
   private conversations, and personal data must never be committed.
5. **Match the existing style.** 2-space indent, CSS variables for all colors,
   `color-mix(in srgb, var(--accent-1) N%, transparent)` for accent tints,
   vanilla JS (no TypeScript, no modules), double quotes in JS.

## How to add a theme (Hermes OS)

1. Add a `:root[data-theme="yourtheme"]` block in the `<style>` section defining the
   **complete** variable set — copy the `ember` block as a template. Required variables:
   `--accent-1`, `--accent-2`, `--bg-1`, `--bg-2`, `--bg-3`, `--text`, `--muted`,
   `--desktop` (background gradient), `--window-glass`, `--accent-ink` (text color
   used on accent-colored surfaces).
2. Add an entry to the `THEMES` array: `{ id: "yourtheme", name: "Display Name",
   colors: ["#accent", "#background"] }` — `colors` drives the gallery swatch.
3. That's it. The Themes app, terminal `theme` command, and localStorage persistence
   pick it up automatically.

## How to add an app (Hermes OS)

Add one entry to the `APPS` object:

```js
myapp: {
  title: "My App",       // window + taskbar + menu label
  glyph: "🚀",           // emoji icon used everywhere
  w: 420, h: 340,        // preferred window size (clamped to viewport)
  render() { return "<h4>…</h4>"; },     // returns the window-body HTML
  onOpen(body) { /* optional: wire up event listeners on the body element */ },
},
```

Desktop icon, start-menu entry, taskbar chip, dragging, minimize/close, and
single-instance behavior are all handled by the window manager automatically.

## Verifying changes

Open the file in any browser and click around. For automated checks, headless
Chromium via Playwright works well (load `file:///…/hermes/index.html`, wait ~2s
for the boot animation, then interact). Things worth asserting: no console errors,
theme switch updates `document.documentElement.dataset.theme` and persists across
reload, windows open/close, terminal commands respond.

## Deployment

- Work on a branch, open a PR to `main`, merge → GitHub Pages redeploys automatically.
- Live URLs: https://voxel-box.github.io and https://voxel-box.github.io/hermes/
- Note: the account also owns a repo named `voxelbox.github.io` (no hyphen). It is a
  placeholder and does NOT serve the site — only `voxel-box.github.io` does. Don't
  publish work there.

## History / context for future sessions

- Hermes OS was first prototyped in claude.ai chats (July 2026) and rebuilt from
  scratch in this repo because chat artifacts aren't retrievable across sessions.
  This repo is now the **source of truth** — treat the code here as canonical and
  evolve it in place rather than rebuilding.
