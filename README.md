# Life Itself Strategy Materials

A wiki/knowledgebase for all [Life Itself][]'s strategy related materials.

[Life Itself]: https://lifeitself.org/

## Structure

- `initiatives/` — one file per initiative. An initiative is an enduring effort that can contain projects. Use stable semantic slugs as filenames (e.g. `second-renaissance.md`).
- `projects/` — one file per project. A project is a bounded effort nested under an initiative. Use `YYYY-` prefixed filenames (e.g. `2024-presenting-our-strategy-v3.md`).
- `visualizations/` — interactive D3 visualizations of the portfolio. Open any HTML file directly in a browser.
- `scripts/` — build tooling. `build-index.js` generates `visualizations/index.js` from markdown frontmatter.

## Data Model

The hierarchy is `initiative → project`. Parent relationships are expressed in frontmatter using wiki-link slugs.

### Frontmatter schema

- Required: `title`, `description`, `created`, `status`
- Optional: `parent`, `tags`, `url`, `github`, `tracker`

`status` values:
- `active` — being actively worked on (whether live or not)
- `maintenance` — live and running but no active development work
- `paused` — temporarily stopped with intention to return
- `idea` — being considered, not yet started
- `archived` — retired or deprecated, no longer pursued

`parent` uses wiki-link style: `parent: [[life-itself]]`

Example:

```yaml
---
title: Second Renaissance
description: Cultural-civilisational renewal project including narrative, events, and movement-building.
created: 2026-01-28
status: active
parent: [[life-itself]]
tags:
  - lifeitself
  - second-renaissance
---
```

### Cross-cutting categorization

Themes and organizational groupings (media, spaces, courses) are metadata, not hierarchy. Use `tags` rather than creating grouping initiatives. This keeps the initiative list as a list of things actually being pursued, not filing cabinet labels.

## Overview of existing materials

![](Excalidraw/materials-overview-2024-02-14.excalidraw.png)

## Inventory of existing strategy materials

See materials sidebar or subfolder.

## Portfolio Visualizations

Interactive views of Life Itself initiatives and projects. Open any HTML file directly in a browser — no server needed.

- [Force-Directed Map](visualizations/portfolio-map.html) — drag, zoom, filter by type. Best for exploring connections.
- [Horizontal Tree](visualizations/portfolio-tree.html) — collapsible dendrogram. Best for parent-child hierarchy.
- [Indented Tree](visualizations/portfolio-indented.html) — file-explorer style list with status and tags.

Data is rebuilt automatically on commit (via a pre-commit hook) whenever initiatives/ or projects/ files change.

<iframe src="visualizations/portfolio-indented.html" width="100%" height="500" style="border:1px solid #ddd; border-radius:8px;"></iframe>

## Building the data index

The visualizations are powered by `visualizations/index.js`, generated from markdown frontmatter by the build script.

```sh
# One-time setup
cd scripts && npm install

# Rebuild manually (also runs automatically on commit)
node scripts/build-index.js
```

The pre-commit hook triggers this automatically when any `initiatives/*.md` or `projects/*.md` file is staged.

## A history of projects to work *on* strategy

- Jun 2024-🔁 (ongoing) - Strategy review and planning 🚧
  - This has somehow metamorphised a bit. Started out as a sync of Rufus & Sylvie and has grown into another strategy evolution.
  - Task: ❌ (TODO)
  - Shaping: missing ...
- Jan 2024-⏸️ - [Presenting our strategy (as is)](projects/2024-presenting-our-strategy-v3.md) 🚧⏸️ status: produced this KB and put most materials and never got to evaluation and publication
  - Summary (from task derived from shaping)
    - Appetite: 3d (reduced by 1d given we spent 1.5d in shaping and work we did in shaping will help)
    - Problem: lot of strategy-related materials but they aren't woven together or consolidated which creates a sense of overwhelm and confusion and prevents them being published and used.
    - Solution: inventory materials, create framework to organize them, create roadmap for publication. If we can, start on consolidated strategy.
  - Task: https://github.com/life-itself/community/issues/1048
  - Pitch: https://github.com/life-itself/comms/blob/main/pitch/2401%20Presenting%20our%20Strategy%20v3%20in%20its%20current%20form.md
- Sep 2021 - Updated and consolidated Core SCQH / logic of existence / theory of change including summary "why Life Itself" - Sep 2021
  - Task: https://github.com/life-itself/community/issues/36
  - Currently we have a large amount of material spread in many areas. We would like a consolidated structure for our SCQHs and at least one root SCQH plus a consolidated summary version so that:
    - We have a clear, simple and short summary for e.g. our front page, for communication
    - We have a organizing structure for our work i.e. any given activity should now be mappable against that hypothesis tree / theory of change
- Nov 2022 (opened) `[uber][epic]` LI v3 Strategy & Implementation 
  - This was the overall task item for doing the v3 strategy
  - Task: https://github.com/life-itself/community/issues/196
    - A10: pretty minimal https://docs.google.com/document/d/1lxWWI4IvnWPLPtQjLY2_fGkko99MnqIDKMCD6E-uDaQ/edit#heading=h.3vdu4snhplyo (could merge to issue)
