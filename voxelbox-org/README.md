# voxelbox-org — source of the live voxelbox.org site

This directory is a **versioned copy of https://voxelbox.org**, captured from the live
site on 2026-07-04 so the code is on GitHub where it can be reviewed, understood, and
edited (by people or AI agents). Before this, the site's source only existed on its host.

> **Important:** GitHub does NOT deploy this directory to voxelbox.org. The live domain
> is hosted elsewhere (served behind Cloudflare). Edits made here must be uploaded to
> that host to appear on the live site. Treat this copy as the working source; keep it
> and the host in sync when publishing changes.

## Structure

- `index.html` — homepage: a scroll-driven "fly through the realm" journey rendered by
  the Three.js voxel scene.
- `servers.html` + one page per server (`minecraft-server.html`, `fivem-server.html`,
  `american-truck-simulator-server.html`, `beammp-server.html`, `palworld-server.html`,
  `satisfactory-server.html`, `enshrouded-server.html`).
- `3d-prints.html` — custom 3D printing service.
- Community: `community.html`, `showcase.html`, `announcements.html`, `partners.html`,
  `team.html`, `update-pings.html`.
- Support & info: `support.html`, `getting-started.html`, `rules.html`, `contact.html`,
  `about.html`, `applications.html`, `costs.html`, `terms.html`, `privacy.html`.
- Shared assets: `voxel.css` (site-wide styles), `voxel.js` (site behavior),
  `voxel-world.js` (3D voxel scene, ES module), `vendor/three.module.js` (Three.js r160),
  `logo.png`, `favicon.ico`, `social-preview.png`.

## Runtime dependencies

- **Google Fonts** (Space Grotesk, Inter) — loaded from fonts.googleapis.com.
- **Live status API** — `https://panel.voxelbox.org/vb-status/status.json` and
  `news.json` power the online/offline dots and news feed. Pages degrade gracefully
  when unreachable.
- `voxel-world.js` is an ES **module** (imports `./vendor/three.module.js`), so pages
  must be served over HTTP — `file://` will not load the 3D scene. For local preview:
  `python3 -m http.server` in this directory.

## Notes for editors

- Cache-busting query strings (`voxel.css?v=8`) and Cloudflare's email-protection
  script were stripped during capture; the contact email is JS-assembled at page load (bot-resistant)
  in `contact.html`.
- voxelbox.org is the canonical source for the server lineup; the landing page and
  Hermes OS at the root of this repo mirror it and must be kept in sync.
- Connection details (IPs/ports) are deliberately absent everywhere — join info
  lives in the Discord so it stays current and off the public record.
