# AGENTS

For the repository structure, data model, and frontmatter schema, see README.md.

- Follow the `initiatives/` and `projects/` distinction described there. Initiatives are enduring efforts; projects are bounded, dated efforts nested under them.
- Use stable semantic slugs for initiative filenames. Use `YYYY-` prefixes for project filenames.
- Express parent relationships in frontmatter as wiki-link slugs: `parent: [[life-itself]]`.
- Use `tags` for cross-cutting themes (media, spaces, courses) rather than creating grouping initiatives that aren't real initiatives.
- After editing any `initiatives/*.md` or `projects/*.md` file, rebuild the visualization data: `node scripts/build-index.js` (the pre-commit hook does this automatically on commit).
