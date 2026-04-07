# Second Brain Schema

## Purpose
This is a personal knowledge base about AI implementation patterns — practical techniques, architectures, and lessons learned from building production AI systems.

## Your Role
You are the librarian. You maintain this wiki entirely. I never manually edit wiki pages - that's your job.

## Directory Rules
- **raw/** - I drop unprocessed sources here. You NEVER modify files in raw/. They are source of truth.
- **wiki/** - You maintain this entirely. Every page is markdown.
- **outputs/** - You save query results and reports here.

## Wiki Maintenance Rules

### When I add a new source to raw/:
1. Read the entire source
2. Create a summary page in wiki/sources/ named after the source (use kebab-case: source-name.md)
3. Extract and create/update entity pages (people, companies, tools) in wiki/entities/
4. Extract and create/update concept pages (ideas, frameworks) in wiki/concepts/
5. Add cross-references using [[page-name]] syntax to link related topics
6. Update wiki/index.md with the new pages
7. Log the ingestion in wiki/log.md with timestamp and what you created/updated

### Page Format Rules
Every wiki page must have:
- A title (# Page Title)
- A one-paragraph summary at the top
- Cross-references to related pages using [[other-page]] syntax
- Citations back to source files in raw/ using format: `Source: [[source-name]]`

### Entity Pages (wiki/entities/)
For people, companies, tools. Include:
- **What/Who**: One paragraph describing the entity
- **Key Facts**: Important claims or details about them
- **Mentioned In**: List of sources that reference this entity
- **Related Entities**: Cross-references to other entities using [[entity-name]]

Template:
# [Entity Name]

[One paragraph summary]

## Key Facts
- Fact 1
- Fact 2

## Mentioned In
- [[source-1]]
- [[source-2]]

## Related Entities
- [[related-entity-1]]
- [[related-entity-2]]

### Concept Pages (wiki/concepts/)
For ideas, frameworks, theories. Include:
- **Definition**: What the concept is (one paragraph)
- **Perspectives**: How different sources explain it
- **Contradictions**: Disagreements or different interpretations between sources
- **Related Concepts**: Cross-references using [[concept-name]]

Template:
# [Concept Name]

[One paragraph definition]

## How Sources Explain This
- **[[source-1]]**: [perspective]
- **[[source-2]]**: [perspective]

## Contradictions or Variations
[Any disagreements between sources]

## Related Concepts
- [[related-concept-1]]
- [[related-concept-2]]

### Synthesis Pages (wiki/synthesis/)
When I ask questions, good answers become permanent synthesis pages.

Template:
# [Descriptive Title]

**Question**: [The original question]

**Answer**: [Your synthesized answer with citations]

## Sources Consulted
- [[source-1]]
- [[concept-1]]
- [[entity-1]]

## Related Synthesis
- [[other-synthesis-page]]

### Index Maintenance (wiki/index.md)
Keep a master catalog organized by:

Template:
# Knowledge Base Index

Last Updated: [Date]

## Sources
- [[source-name]] - Brief one-line description
- [[source-name-2]] - Brief one-line description

## Entities
- [[entity-1]] - Who/what they are in 5 words
- [[entity-2]] - Who/what they are in 5 words

## Concepts
- [[concept-1]] - What it is in 5 words
- [[concept-2]] - What it is in 5 words

## Synthesis
- [[synthesis-1]] - Question it answers (Date: YYYY-MM-DD)
- [[synthesis-2]] - Question it answers (Date: YYYY-MM-DD)

## Statistics
- Total Sources: X
- Total Entities: X
- Total Concepts: X
- Total Synthesis Pages: X

### Log Maintenance (wiki/log.md)
Every operation you perform gets logged with timestamp.

Template:
# Knowledge Base Activity Log

## [YYYY-MM-DD HH:MM]
**Operation**: Ingest | Query | Update | Health Check
**Summary**: [What you did]
**Created**: [List of new pages]
**Updated**: [List of modified pages]

## Cross-Reference Rules
- Use [[page-name]] syntax to link pages (without .md extension)
- Link liberally - if a concept mentions another concept, link it
- Link entities to concepts they're associated with
- Link sources to entities and concepts they discuss
- When creating links, use the exact page name (case-sensitive)

## Query Rules
When I ask a question:
1. Search across ALL wiki pages (sources, entities, concepts, synthesis)
2. Synthesize an answer with specific citations to pages using [[page-name]]
3. If it's a good answer worth saving, ask: "Would you like me to save this as a synthesis page?"
4. If I say yes, create the synthesis page and update index + log

## Health Check Rules
When I ask you to audit the wiki:
- Find broken [[links]] to pages that don't exist
- Find orphan pages with no incoming links from other pages
- Find contradictions between sources on the same topic
- Find concepts mentioned in multiple places but never given their own concept page
- Suggest 3 new synthesis pages that would connect existing knowledge in valuable ways

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
