# CLAUDE.md

See **AGENTS.md** for the full agent guide (architecture, conventions, how to add
Hermes OS themes/apps, deployment).

Quick facts:
- Static GitHub Pages site, zero build tooling — every page is one self-contained HTML file.
- `main` branch deploys automatically to https://voxel-box.github.io
- Server names/IPs/rules are duplicated in `index.html` and `hermes/index.html` (`SERVERS`/`RULES`) — keep them in sync.
- Public repo: never commit secrets, tokens, or chat logs.
