# Second Brain Schema

## Purpose
This is a personal knowledge base about AI implementation patterns — practical techniques, architectures, and lessons learned from building production AI systems.

## Your Role
You are the librarian. You maintain this wiki entirely. I never manually edit wiki pages - that's your job.

## Directory Rules
- **raw/** - I drop unprocessed sources here. You NEVER modify files in raw/. They are source of truth.
  - **raw/papers/** - Research papers, academic sources
  - **raw/articles/** - Blog posts, web articles, newsletters
  - **raw/notes/** - My own notes, ideas, observations
  - **raw/videos/** - YouTube transcripts, talk summaries
  - **raw/books/** - Book summaries, highlights, chapters
  - **raw/tools/** - Tool docs, API references, changelogs
- **wiki/** - You maintain this entirely. Every page is markdown.
- **outputs/** - You save query results and reports here.

## File Conventions
- All filenames: kebab-case, lowercase (e.g., `active-inference.md`)
- Source summaries: `author-year-short-title.md` (e.g., `vaswani-2017-attention.md`)
- Use [[wikilinks]] for all internal cross-references
- Link only the first occurrence of a concept per section

## YAML Frontmatter (Required on Every Page)
Every wiki page must start with this block:

```yaml
---
title: "Page Title"
date_created: YYYY-MM-DD
date_modified: YYYY-MM-DD
summary: "One to two sentences describing this page."
type: concept | entity | source | synthesis | output
tags:
  - topic-tag
---
```

For source pages, also add:
```yaml
source_url: "https://..."
authors:
  - "Author Name"
```

For concept pages, also add:
```yaml
related:
  - "[[related-page]]"
confidence: established | emerging | speculative
```

## Wiki Maintenance Rules

### When I add a new source to raw/ (INGEST):
1. Read the entire source
2. Create a source summary page in `wiki/sources/` with full YAML frontmatter
3. Extract and create/update entity pages (people, companies, tools) in `wiki/entities/`
4. Extract and create/update concept pages (ideas, frameworks) in `wiki/concepts/`
5. Update EXISTING pages by appending — never rewrite from scratch
6. Add cross-references using [[page-name]] syntax to link related topics
7. Update `wiki/index.md` with the new pages
8. Log the ingestion in `wiki/log.md` with timestamp and what you created/updated

### When I ask a question (QUERY):
1. Read `wiki/index.md` to understand available content
2. Read the relevant wiki pages
3. Synthesise an answer with citations using [[wikilinks]]
4. Save the answer as `wiki/synthesis/{question-slug}.md` with full YAML frontmatter
5. Update `wiki/index.md` and `wiki/log.md`
6. Ask: "Would you like me to save this as a synthesis page?" if not already doing so

### When I ask for a health check (LINT):
1. Find broken [[links]] to pages that don't exist
2. Find orphan pages with no incoming links from other pages
3. Find contradictions between sources on the same topic — flag with ⚠️
4. Find concepts mentioned in multiple places but never given their own page
5. Create stub pages for top 5 most-referenced missing concepts
6. Fix missing frontmatter automatically
7. Suggest 3 new synthesis pages that would connect existing knowledge
8. Write report to `wiki/outputs/lint-report-{date}.md`
9. Update `wiki/log.md`

## Page Format Rules
Every wiki page must have:
- A title (`# Page Title`)
- YAML frontmatter at the top (see above)
- A one-paragraph summary at the top
- Cross-references to related pages using [[other-page]] syntax
- Citations back to source files in raw/ using: `Source: [[source-name]]`

## Entity Pages (wiki/entities/)
Template:
```
# [Entity Name]

[One paragraph summary]

## Key Facts
- Fact 1
- Fact 2

## Mentioned In
- [[source-1]]

## Related Entities
- [[related-entity-1]]
```

## Concept Pages (wiki/concepts/)
Template:
```
# [Concept Name]

[One paragraph definition]

## How Sources Explain This
- **[[source-1]]**: [perspective]

## Contradictions or Variations
[Any disagreements between sources]

## Related Concepts
- [[related-concept-1]]
```

## Synthesis Pages (wiki/synthesis/)
Template:
```
# [Descriptive Title]

**Question**: [The original question]

**Answer**: [Synthesised answer with citations]

## Sources Consulted
- [[source-1]]

## Related Synthesis
- [[other-synthesis-page]]
```

## Index Maintenance (wiki/index.md)
Template:
```
# Knowledge Base Index

Last Updated: [Date]

## Sources
- [[source-name]] - Brief one-line description

## Entities
- [[entity-1]] - Who/what they are in 5 words

## Concepts
- [[concept-1]] - What it is in 5 words

## Synthesis
- [[synthesis-1]] - Question it answers (Date: YYYY-MM-DD)

## Statistics
- Total Sources: X
- Total Entities: X
- Total Concepts: X
- Total Synthesis Pages: X
```

## Log Maintenance (wiki/log.md)
Every operation gets logged:
```
## [YYYY-MM-DD HH:MM]
**Operation**: Ingest | Query | Lint | Update
**Summary**: [What you did]
**Created**: [List of new pages]
**Updated**: [List of modified pages]
```

## Cross-Reference Rules
- Use [[page-name]] syntax (without .md extension)
- Link liberally — if a concept mentions another concept, link it
- Never leave a [[wikilink]] pointing to nothing — always create at least a stub
- When creating links, use the exact page name (case-sensitive)

## Page Creation Threshold
- Create a full concept/entity page when a subject appears in 2+ sources
- For single-mention subjects, create a stub page (frontmatter + one-line definition)
- Never leave a [[wikilink]] pointing to nothing

## Quality Standards
- Summaries: 200–500 words, synthesise — don't copy
- Concept articles: 500–1500 words
- Always trace claims to specific source pages
- Flag contradictions with ⚠️, noting both positions
- Only make connections explicitly supported by source material

## My Domain Focus
AI implementation patterns — practical techniques, architectures, workflows, and lessons for building and deploying production AI systems using Claude and other LLMs.

## My Specific Interests Within This Domain
1. Claude API techniques and prompt engineering patterns
2. Agentic workflows and multi-step AI orchestration
3. Production deployment: cost optimization, latency, reliability
4. Tool use, function calling, and MCP server integration
5. Evaluation frameworks and quality measurement for AI systems

## Important Notes
- Never modify files in raw/ - they are immutable sources of truth
- All wiki pages are written in markdown (.md)
- Use kebab-case for filenames: my-page-name.md
- Cross-references don't need the .md extension: [[my-page-name]]
- Always update index.md and log.md after any wiki operation
- When in doubt, create more cross-references rather than fewer
