# Life Itself Strategy

A working repository for [Life Itself][]'s strategy — developing where we're going and why, and keeping an overview of the portfolio of activities that expresses that strategy.

[Life Itself]: https://lifeitself.org/

Two main purposes:

1. **Develop strategy** — working space for thinking through, drafting, and archiving Life Itself's strategy materials (SCQHs, theories of change, narratives, plans)
2. **Portfolio overview** — a structured, living map of our initiatives and projects to support strategy work and give a clear picture of what we're doing

## Portfolio of Initiatives & Projects

Interactive views of Life Itself initiatives and projects. Open any HTML file directly in a browser — no server needed.

- [Force-Directed Map](visualizations/portfolio-map.html) — drag, zoom, filter by type. Best for exploring connections.
- [Horizontal Tree](visualizations/portfolio-tree.html) — collapsible dendrogram. Best for parent-child hierarchy.
- [Indented Tree](visualizations/portfolio-indented.html) — file-explorer style list with status and tags.

<iframe src="visualizations/portfolio-indented.html" width="100%" height="500" style="border:1px solid #ddd; border-radius:8px;"></iframe>

The underlying data lives in `initiatives/` and `projects/`. The index is rebuilt automatically on commit whenever those files change.

## Strategy Materials

`materials/` is an archive of pre-existing strategy documents — SCQHs, theories of change, narratives, plans and reviews going back to 2017. See [materials/README.md](materials/README.md) for a full index.

Key working documents at root level:

- [Strategy v3 consolidated](Strategy%20v3%20consolidated.md)
- [Strategy v2 consolidated](Strategy%20v2%20consolidated.md)
- [Framework for strategy and strategy materials](Framework%20for%20strategy%20and%20strategy%20materials.md)

### Overview of existing materials

![](Excalidraw/materials-overview-2024-02-14.excalidraw.png)

## History of strategy work

A log of projects to work *on* strategy itself:

- **Jun 2024–ongoing** — Strategy review and planning (ongoing)
- **Jan 2024** ⏸️ — [Presenting our strategy (as is)](projects/2024-presenting-our-strategy-v3.md) — produced this KB and most materials; never reached evaluation and publication
  - Appetite: 3d; Problem: lots of strategy materials not woven together, creating overwhelm; Solution: inventory, organise, create roadmap for publication
  - Task: https://github.com/life-itself/community/issues/1048 · Pitch: [shaping doc](https://github.com/life-itself/comms/blob/main/pitch/2401%20Presenting%20our%20Strategy%20v3%20in%20its%20current%20form.md)
- **Sep 2021** — Updated and consolidated Core SCQH / logic of existence / theory of change
  - Task: https://github.com/life-itself/community/issues/36
- **Nov 2022** — LI v3 Strategy & Implementation `[uber][epic]`
  - Task: https://github.com/life-itself/community/issues/196

## Working on this repo

See [AGENTS.md](AGENTS.md) for the full data model, frontmatter schema, file conventions, status values, and build instructions.
