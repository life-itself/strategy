# Portfolio Site Links Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Make portfolio map clicks and tree row view links open the local Flowershow page for each initiative or project instead of any external project URL.

**Architecture:** Derive a local site path from each repo-relative markdown file path during portfolio index generation, then have both visualizations use that field. Keep external `url` metadata unchanged so the data model still retains off-site links separately from on-site navigation.

**Tech Stack:** Static HTML, browser JavaScript, Node.js build script, Node test runner

---

### Task 1: Add a tested site-path helper

**Files:**
- Create: `portfolio/scripts/site-path.js`
- Create: `portfolio/scripts/site-path.test.js`

**Step 1: Write the failing test**

Add tests covering:
- `initiatives/example.md` -> `/initiatives/example`
- `projects/2026-example.md` -> `/projects/2026-example`
- null/empty input -> null

**Step 2: Run test to verify it fails**

Run: `node --test portfolio/scripts/site-path.test.js`
Expected: FAIL because the helper does not exist yet.

**Step 3: Write minimal implementation**

Export a function that strips the `.md` suffix and prefixes the result with `/`.

**Step 4: Run test to verify it passes**

Run: `node --test portfolio/scripts/site-path.test.js`
Expected: PASS

### Task 2: Emit local site paths in generated portfolio data

**Files:**
- Modify: `portfolio/scripts/build-index.js`
- Modify: `portfolio/index.js`

**Step 1: Update index generation**

Import the new helper and assign `sitePath` on each entry from `file`.

**Step 2: Rebuild generated data**

Run: `node portfolio/scripts/build-index.js`
Expected: `portfolio/index.js` updated with `sitePath` for each entry.

### Task 3: Update both visualizations to use the local site path

**Files:**
- Modify: `portfolio/portfolio-map.html`
- Modify: `portfolio/portfolio-indented.html`
- Modify: `portfolio/README.md`

**Step 1: Map navigation**

Make node clicks navigate to `sitePath` in the current tab and update the copy to describe local page navigation.

**Step 2: Tree row affordance**

Keep row click for collapse/expand. Add a separate `View` link control per row that opens the local page without toggling the row.

**Step 3: Documentation**

Update the README interaction text to describe the new local-page behavior.

### Task 4: Verify end-to-end behavior

**Files:**
- Test: `portfolio/scripts/site-path.test.js`

**Step 1: Run automated test**

Run: `node --test portfolio/scripts/site-path.test.js`
Expected: PASS

**Step 2: Rebuild portfolio index**

Run: `node portfolio/scripts/build-index.js`
Expected: regenerated `portfolio/index.js` with `sitePath`

**Step 3: Sanity-check output**

Inspect representative entries in `portfolio/index.js` and confirm `sitePath` matches the markdown path without `.md`.
