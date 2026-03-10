# QuickQuote — Stack Decisions

**Date:** 2025-11-14

---

## Architecture

**Pattern:** Single-page local app (no backend)
**Rationale:** The user is a solo field rep who needs this to work offline and
without IT setup. A backend would add deployment complexity and login friction
that the PRD explicitly rules out.

---

## Runtime & Language

Vanilla JavaScript + HTML + CSS. No build step.
Rationale: No toolchain to install, no build to run, no deployment pipeline.
Open `index.html` in a browser and it works.

---

## Key Dependencies

| Package | Purpose |
|---|---|
| None | No external dependencies for v1 |

> PDF export handled via `window.print()` + print stylesheet. No library needed.

---

## Data Layer

**Choice:** localStorage
**Rationale:** Price list and any saved quotes persist between sessions without
a server. No sync needed — this is a single-user tool.

---

## Agents & MCPs

None — this project does not use AI agents or MCP tools.

---

## Deployment

**Target:** Local file system / static hosting
**Method:** Open `index.html` directly, or drop on any static host (GitHub Pages,
Netlify, Cloudflare Pages) if web access is needed later.

---

## Explicitly NOT Using

| Technology | Reason |
|---|---|
| React / Vue / Svelte | No build step requirement; vanilla is sufficient |
| Node.js backend | Local-first requirement; no server |
| SQLite | Overkill for localStorage-scale data |
| Paid PDF library | Browser print dialog covers v1 needs |

---

## Open Technical Questions

None.
