---
description: Health check the wiki — find broken links, orphans, contradictions, gaps, and fix what you can
allowed-tools: Read, Write, Bash, Glob, Grep
---

# Wiki Lint

Read CLAUDE.md for project conventions. Then perform a full health check on `wiki/`.

Check for and report the following:

1. **CONTRADICTIONS** — claims in one page that conflict with another. List both pages and the conflicting claims.

2. **ORPHAN PAGES** — pages in wiki/ with no inbound [[wikilinks]] from other pages. List them and suggest where to add links.

3. **MISSING PAGES** — [[wikilinks]] that appear in pages but have no corresponding file. Create stub pages for the top 5 most-referenced missing pages.

4. **BROKEN LINKS** — [[wikilinks]] pointing to files that don't exist. List them.

5. **INCOMPLETE METADATA** — pages missing a title, summary, or source citation. Fix them automatically.

6. **STALE CONTENT** — pages whose source material is likely outdated (flag anything that references events/dates over 6 months old with no recent updates).

7. **SUGGESTED QUESTIONS** — based on the current wiki content, suggest 3–5 research questions worth exploring next.

Fix everything you can automatically (stubs, metadata, simple link fixes).
For contradictions and major gaps, write a full report to `wiki/outputs/lint-report-{today's date}.md`.
Update `wiki/log.md` with the lint operation.
