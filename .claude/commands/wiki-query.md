---
description: Research a question across the wiki and file the answer back as a synthesis page
allowed-tools: Read, Write, Bash, Glob, Grep
---

# Wiki Query

Read CLAUDE.md for project conventions.

The user's question is everything after `/wiki-query` in the prompt.

Steps:
1. Read `wiki/index.md` to understand what content exists
2. Identify which wiki pages are relevant to the question
3. Read those specific pages (concepts, entities, sources as needed)
4. Synthesise a comprehensive answer:
   - Cite specific wiki pages using [[wikilinks]]
   - Flag any gaps where the wiki lacks information with ⚠️
   - Note if sources contradict each other
5. Save the answer to `wiki/synthesis/` with a descriptive kebab-case filename
6. Update `wiki/index.md` — add the new synthesis page under the Synthesis section
7. Append to `wiki/log.md`

The answer should be a permanent wiki page, not a throwaway response.
Format it as a proper synthesis page with:
- A clear title
- The original question
- A synthesised answer with citations
- A "Sources Consulted" section listing all [[wikilinks]] referenced
