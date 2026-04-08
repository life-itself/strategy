---
title: Portfolio Map
description: Interactive visualizations of Life Itself initiatives, projects and ideas — and the data model behind them.
created: 2026-04-07
status: active
parent: life-itself-management
tags:
  - visualization
  - portfolio
---

Build and maintain interactive visualizations of Life Itself's portfolio of initiatives and projects. The data lives in markdown files (initiatives/, projects/) with frontmatter; a build script generates a JS data file; HTML visualizations render it using D3.

The name "portfolio map" is preferred over "initiatives map" since the scope includes initiatives, projects, and ideas.

## Jobs to be done

### Situation

- Life Itself does not currently have a clear, current map of its initiatives and projects.
- Existing overviews are incomplete or out of date, including material that could be shared externally.
- We need a practical overview of current and potential work as input to 2026 strategy conversations.

### Complication

- Without a current portfolio map, strategic planning is harder to do systematically: it is difficult to assess what to continue, pause, merge, prioritize, or resource.
- Newer team members and collaborators lack an easy way to understand what Life Itself is doing now.
- Any shareable external view is harder to maintain because the underlying portfolio picture is fragmented and stale.

### Question

- How do we create a simple, current, and maintainable portfolio map quickly, in a form that supports 2026 strategic decision-making, helps orient team members, and can also be adapted for external sharing?

### Hypothesis

- A markdown-based portfolio database, with initiatives and projects modeled separately, will give us a lightweight source of truth that is easy to update.
- From that source, we can generate simple visualizations and add fields over time, such as owners, status, or resource needs, without rebuilding the system from scratch.

## Tasks

- [ ] What is purpose
- [ ] Add all the initiatives
- [ ] How to do groupings ...

## Current state

Three visualizations exist in `visualizations/`:

- **Force-Directed Map** (`portfolio-map.html`) — draggable node graph, best for exploring connections
- **Horizontal Tree** (`portfolio-tree.html`) — collapsible dendrogram, best for hierarchy
- **Indented Tree** (`portfolio-indented.html`) — file-explorer style, best for dense overview

All work locally via `file://` (no server needed). Data is built from markdown frontmatter by `scripts/build-index.js` into `visualizations/index.js`.

## Armelle's portfolio-map.html

A separate visualization (`portfolio-map.html` at repo root) was built as "Armelle's View". It introduces several additions worth evaluating.

### New entries (no backing markdown file)

| Slug | Title | Purpose |
|------|-------|---------|
| `spaces-and-community` | Spaces & Community | Umbrella grouping |
| `bergerac-hub` | Bergerac Hub | New initiative |
| `media` | Media & Communications | Umbrella grouping |
| `podcasts` | Podcasts | Sub-grouping under media |
| `second-renaissance-magazine` | Second Renaissance Magazine | New initiative |
| `projects-hub` | Projects | Virtual grouping for a "projects flower" view |

It also duplicates every project as `proj-*` entries re-parented under `projects-hub` to create a second visual cluster.

### New data attributes

| Attribute | Purpose |
|-----------|---------|
| `category` | Distinguishes "maintenance" (ongoing, no deliverable) from "initiative" |
| `umbrella` | Color-coded cluster grouping (pink, purple, teal, coral) |
| `owners` | Reference person / responsible party |
| `people` | Other people involved (currently empty) |
| `fillColor` | Visual color tied to umbrella membership |
| `secondary_parents` | Additional parent links for multi-parent items |
| `deadline` | Project deadline (currently empty) |
| `cadence` | Meeting/check-in cadence (currently empty) |

### Changed parent links vs our markdown

- `life-itself-hubs` → `spaces-and-community` (was `life-itself`)
- `life-itself-podcast`, `microcasts`, `over-the-mountains` → `podcasts` (were `life-itself`)
- `2026-intro-to-life-itself-videos`, `life-itself-websites-2025` → `media` (were `life-itself` / `life-itself-management`)
- `life-itself-practicum` → `life-itself-courses` (was `life-itself`)
- `teal-estate` → `spaces-and-community` (was `developmental-spaces-dds`)

## Design question: initiatives as groupings?

The Armelle view creates umbrella "initiatives" (Spaces & Community, Media & Communications, etc.) that aren't really initiatives — they're domains of activity used to organize the tree. This is convenient but problematic.

### Pros

- Simple: one mechanism (parent links) handles everything, no new concepts
- Visualizations just work without changes
- Pragmatic; uses existing infrastructure

### Cons

- **Semantic confusion**: some "initiatives" are things you're actively doing (Praxis Ecology, 2RCon) while others are just filing cabinets. Harder to answer "what are we actually working on?"
- **Forces a single taxonomy**: Over the Mountains is both media and second-renaissance. The `secondary_parents` field is already patching around trees not being expressive enough.
- **Inflates initiative count**: undermines using that count as a signal of scope/load.

### Recommended approach: use tags for cross-cutting categorization

Keep initiatives as real initiatives with goals and outcomes. Use **tags** in frontmatter for cross-cutting categories like `domain: media`, `domain: spaces`. The visualizations can group by tag when that view is wanted, while the parent tree stays a clean hierarchy of actual work.

This is more honest to the data and supports multiple classifications without forcing a single tree. The `umbrella` and `category` fields in the Armelle view are essentially reinventing tags — a sign the single-tree model was already straining.

### What to integrate

Worth adding to our markdown files:

- `category`: distinguishing maintenance from initiative is genuinely useful
- `owners`: valuable for accountability
- `bergerac-hub` and `second-renaissance-magazine`: real initiatives that should have markdown files
- `life-itself-practicum` reparenting to `life-itself-courses`: this correction makes sense

Not worth adding:

- Umbrella grouping initiatives (spaces-and-community, media, podcasts, projects-hub): use tags instead
- `fillColor` / `umbrella`: purely visual, let the visualization derive these from tags
- `proj-*` duplicates: a visualization concern, not a data concern
