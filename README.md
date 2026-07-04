# Voxelbox — voxel-box.github.io

The website for the **Voxelbox game server network**, served by GitHub Pages at
**https://voxel-box.github.io**.

## What's here

| Path | What it is |
| --- | --- |
| `index.html` | The main Voxelbox site: server list with IPs, per-server Rules Hub, community section. |
| `hermes/index.html` | **Hermes OS** — a browser "desktop" hub for the network: draggable windows, taskbar, start menu, and apps (Servers, Rules Hub, Notes, Terminal, About) plus a six-theme theming engine. |
| `AGENTS.md` | Instructions for AI coding agents working on this repo (conventions, architecture, how to extend things). |

## How it works

- **No build step, no dependencies.** Every page is a single self-contained HTML file
  with inline CSS and vanilla JavaScript. To develop, just open the file in a browser.
- **Deployment is automatic.** GitHub Pages serves the `main` branch — anything merged
  to `main` is live within a minute or two.
- **State is local.** Hermes OS stores the chosen theme and notes in the visitor's
  `localStorage`; nothing is sent anywhere.

## The network

Seven servers: Minecraft, StarRupture, BeamMP, Sons of the Forest, Enshrouded,
Palworld, and Satisfactory. Server names, IPs, and rules live in two places that
must be kept in sync when they change:

1. `index.html` — the `#servers` and `#rules` sections
2. `hermes/index.html` — the `SERVERS` and `RULES` constants at the top of the script

## Theming

Hermes OS themes are pure CSS-variable sets on `:root[data-theme="…"]`.
Available themes: `ember` (default, Voxelbox orange), `midnight`, `frost`,
`verdant`, `synthwave`, `daylight` (light mode). See `AGENTS.md` for how to add one.
