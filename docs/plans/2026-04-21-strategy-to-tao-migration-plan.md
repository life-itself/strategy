---
created: 2026-04-21
authors: [rufus-pollock]
---

# Migration Plan: strategy repo → tao

Companion to [`docs/plans/2026-04-21-great-convergence.md`](./2026-04-21-great-convergence.md).

**Goal:** merge all content from [`life-itself/strategy`](https://github.com/life-itself/strategy) into [`life-itself/tao`](https://github.com/life-itself/tao), making tao the single knowledge base for Life Itself. Archive or redirect the strategy repo once complete.

---

## Repos

- Strategy repo on disk: `~/src/lifeitself/strategy`
- Tao repo on disk: `~/src/lifeitself/tao`
- Strategy repo remote: https://github.com/life-itself/strategy
- Tao repo remote: https://github.com/life-itself/tao
- Tao site: https://tao.lifeitself.org

---

## Proposed folder mapping

Top-level tao structure after migration:

```
initiatives/        ← what Life Itself does — top-level, most-accessed
portfolio/          ← map/view of initiatives + scripts — top-level
projects/           ← top-level
plans/              ← already exists; absorb strategy weekly plans
meetings/           ← new top-level folder
people/             ← new top-level folder
strategy/           ← thinking layer: analysis docs, archive, log
  docs/
  archive/
  log/
  calendar/
  templates/
```

`strategy/` is intentionally narrow — it holds the *thinking and analysis layer*, not live operational content. Initiatives, portfolio, projects, plans, meetings, and people are all top-level because they are what people navigate to directly.

| Strategy repo | → Tao destination | Notes |
|---|---|---|
| `initiatives/` | `initiatives/` | Top-level — what Life Itself does |
| `portfolio/` | `portfolio/` | Top-level — map/view + scripts |
| `projects/` | `projects/` | Top-level |
| `docs/` | `strategy/docs/` | Planning docs and strategic analysis |
| `materials/` | `strategy/archive/` | Historical strategy archive |
| `Strategy v2 consolidated.md` | `strategy/archive/` | Historical |
| `Strategy v3 consolidated.md` | `strategy/archive/` | Historical |
| `Framework for strategy and strategy materials.md` | `strategy/archive/` | Historical |
| `Materials Template Documentation.md` | `strategy/archive/` | Historical |
| `log/` | `strategy/log/` | Outflow and raw notes |
| `plans/` | `plans/` | Merge with tao's existing `plans/` folder |
| `meetings/` | `meetings/` | New top-level folder; tao's `meetings.md` becomes its index |
| `people/` | `people/` | New top-level folder |
| `Excalidraw/` | `excalidraw/` | Tao already has `exalidraw/` — merge, normalise to lowercase |
| `assets/` | `assets/` | Merge into tao's existing `assets/` |
| `calendar/` | `strategy/calendar/` | Or drop if unused |
| `Templates/` | `strategy/templates/` | Or integrate into relevant sections |
| `sandbox/` | Drop | Not worth migrating |
| `AGENTS.md` | `AGENTS.md` | Update for tao context — see notes below |
| `config.json` | Merge into tao `config.json` | Add new nav sections — see notes below |

---

## Step-by-step instructions

### Step 0: Verify both repos are clean and up to date

```bash
cd ~/src/lifeitself/strategy && git status && git pull
cd ~/src/lifeitself/tao && git status && git pull
```

Both should be on `main` with no uncommitted changes before starting.

---

### Step 1: Create the new folder structure in tao

In `~/src/lifeitself/tao`, create the following new directories:

```
strategy/
strategy/initiatives/
strategy/portfolio/
strategy/projects/
strategy/docs/
strategy/archive/
strategy/log/
strategy/calendar/
strategy/templates/
meetings/
people/
```

---

### Step 2: Copy content from strategy into tao

Copy each folder as follows. Use `cp -r` (not `mv`) so the strategy repo stays intact until the migration is verified.

```bash
# Top-level operational content
cp -r ~/src/lifeitself/strategy/initiatives/. ~/src/lifeitself/tao/initiatives/
cp -r ~/src/lifeitself/strategy/portfolio/. ~/src/lifeitself/tao/portfolio/
cp -r ~/src/lifeitself/strategy/projects/. ~/src/lifeitself/tao/projects/

# Strategy thinking layer
cp -r ~/src/lifeitself/strategy/docs/. ~/src/lifeitself/tao/strategy/docs/
cp -r ~/src/lifeitself/strategy/log/. ~/src/lifeitself/tao/strategy/log/

# Archive
cp -r ~/src/lifeitself/strategy/materials/. ~/src/lifeitself/tao/strategy/archive/
cp "~/src/lifeitself/strategy/Strategy v2 consolidated.md" ~/src/lifeitself/tao/strategy/archive/
cp "~/src/lifeitself/strategy/Strategy v3 consolidated.md" ~/src/lifeitself/tao/strategy/archive/
cp "~/src/lifeitself/strategy/Framework for strategy and strategy materials.md" ~/src/lifeitself/tao/strategy/archive/
cp "~/src/lifeitself/strategy/Materials Template Documentation.md" ~/src/lifeitself/tao/strategy/archive/

# Plans — merge into existing tao plans folder
cp -r ~/src/lifeitself/strategy/plans/. ~/src/lifeitself/tao/plans/

# Meetings — new folder
cp -r ~/src/lifeitself/strategy/meetings/. ~/src/lifeitself/tao/meetings/

# People — new folder
cp -r ~/src/lifeitself/strategy/people/. ~/src/lifeitself/tao/people/

# Assets — merge
cp -r ~/src/lifeitself/strategy/assets/. ~/src/lifeitself/tao/assets/

# Excalidraw — merge into tao's existing exalidraw folder (note spelling difference)
cp -r ~/src/lifeitself/strategy/Excalidraw/. ~/src/lifeitself/tao/excalidraw/

# Calendar (if it has content worth keeping)
cp -r ~/src/lifeitself/strategy/calendar/. ~/src/lifeitself/tao/strategy/calendar/
```

Do **not** copy: `sandbox/`, `portfolio/scripts/node_modules/` (re-install dependencies instead).

---

### Step 3: Update internal links

After copying, run a search for links pointing to the old strategy repo or using old relative paths, and update them to the new tao paths.

Key things to check:

- Any `../../` or `../` relative links in copied docs that assumed the old folder structure
- Links to `https://github.com/life-itself/strategy/` — update to `https://github.com/life-itself/tao/` with new paths
- The `great-convergence.md` and `team-coordination-hub-notes.md` docs (now at `strategy/docs/plans/`) reference each other and reference `meetings/` — update those relative paths

A quick grep to find candidates:
```bash
grep -r "life-itself/strategy" ~/src/lifeitself/tao --include="*.md" -l
grep -r "\.\./\.\." ~/src/lifeitself/tao/strategy --include="*.md" -l
```

---

### Step 4: Update tao navigation and index

**`tao/config.json`**: add navigation entries for the new sections. Look at the existing `config.json` structure and add:
- Strategy (linking to `strategy/`)
- Initiatives (linking to `strategy/initiatives/`)
- Portfolio (linking to `strategy/portfolio/`)
- Plans (already exists — verify it still works after merge)
- Meetings (linking to `meetings/`)
- People (linking to `people/`)

**`tao/index.md`**: add a "Strategy and portfolio" section linking to:
- Portfolio map (`strategy/portfolio/`)
- Initiatives (`strategy/initiatives/`)
- Weekly plans (`plans/`)
- Meeting notes (`meetings/`)

**`tao/plans.md`**: update to point to the merged `plans/` folder. The existing file links to historical plans (`plan-2018.md` etc.) — extend it to also link to the weekly plans now in the same folder.

**`tao/meetings.md`**: this currently appears to be a stub or page. Convert it (or create `meetings/index.md`) to index the meeting notes now in the `meetings/` folder.

---

### Step 5: Update AGENTS.md

The strategy repo has an `AGENTS.md` with instructions for AI agents. Copy this to tao root and update:
- Update any repo-specific references (paths, GitHub URLs) to reflect tao
- Check if tao already has an `AGENTS.md` and merge if so

---

### Step 6: Verify the tao site builds

```bash
cd ~/src/lifeitself/tao
# install deps if needed
npm install
# run local dev server and check:
# - index page loads and new links work
# - strategy/initiatives/ pages render
# - strategy/portfolio/ page renders
# - plans/ and meetings/ pages render
# - no broken internal links
```

Check for broken links using whatever link-checking tooling is available.

---

### Step 7: Commit to tao

```bash
cd ~/src/lifeitself/tao
git add .
git commit -m "feat: migrate strategy repo content into tao

Brings portfolio, initiatives, plans, meetings, people, projects, and
historical strategy archive from life-itself/strategy into tao as the
single Life Itself knowledge base. See great-convergence plan for rationale."
```

---

### Step 8: Push and verify live site

```bash
git push origin main
```

Check https://tao.lifeitself.org once deployed — verify key pages load, especially portfolio and initiatives.

---

### Step 9: Archive the strategy repo

Once migration is verified on the live tao site:

1. Update `strategy` repo `README.md` to say: *"This repo has been merged into [life-itself/tao](https://github.com/life-itself/tao). This repo is now archived."*
2. Add a redirect or notice at the top of key pages (`portfolio/README.md`, `initiatives/` etc.) pointing to tao.
3. Archive the repo on GitHub: Settings → Danger Zone → Archive this repository.

Do **not** delete the strategy repo — keep it as a read-only archive for git history and any inbound links.

---

## What to watch out for

- **`portfolio/scripts/node_modules/`** — do not copy this. Run `npm install` in the new location instead.
- **Excalidraw folder name** — strategy uses `Excalidraw/` (capital E), tao uses `exalidraw/` (lowercase). Merge into lowercase.
- **`config.json` conflicts** — both repos have a `config.json` for the Flowershow site. Do not overwrite tao's config; manually merge the relevant nav entries.
- **`plans/README.md`** — strategy repo has one; tao has `plans.md` at root. Check for content overlap before copying.
- **People profiles** — check if tao already has any people content before copying `people/` wholesale.
- **GitHub issues** — strategy repo may have open issues. Review and either close, move manually to `community` repo, or open equivalent issues in `tao` before archiving.
