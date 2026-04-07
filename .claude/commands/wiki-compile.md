---
description: Compile all new raw/ sources into the wiki (sources, concepts, entities, index, log)
allowed-tools: Read, Write, Bash, Glob, Grep
---

# Wiki Compile

Read CLAUDE.md for project conventions.

1. Glob `raw/**/*.md` to find ALL source files
2. Glob `wiki/sources/**/*.md` to find already-processed sources
3. Diff the two lists to identify NEW (unprocessed) sources
4. For each NEW source:
   a. Create a source summary in `wiki/sources/`
   b. Identify key concepts and entities mentioned
   c. Create new concept pages in `wiki/concepts/` if they don't exist
   d. Create new entity pages in `wiki/entities/` if they don't exist
   e. Update EXISTING pages by appending new info (never rewrite from scratch)
   f. Add [[wikilinks]] between all related pages
5. Regenerate `wiki/index.md` with all pages listed and one-line summaries
6. Append all operations to `wiki/log.md` with today's date
7. Report: how many sources processed, pages created, pages updated

If no new sources found, say so and exit cleanly.
