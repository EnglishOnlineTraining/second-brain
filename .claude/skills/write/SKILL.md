---
name: write
description: Retrieve grounded context from the second-brain wiki pages and draft a report, presentation, document, template, or summary into pages/output-*.md. Use whenever Shaun says "/write report/presentation/document/summary '<topic>'", asks for a write-up grounded in what's already been ingested, or wants an artifact produced from the knowledge base.
---

# /write — Retrieve Context → Draft Artifact

**Trigger:** User requests a report, presentation, document, template, or summary.

**Usage**
```
/write report "topic"
/write presentation "topic"
/write summary "topic"
```

## Workflow

1. **Retrieve context**
   - Search `pages/wiki-*` for relevant concepts, people, literature, permanent-notes.
   - Read the most relevant pages fully.
   - Note contradictions, gaps, weak evidence.

2. **Draft**
   - Choose a starter from `pages/templates-output-{report|presentation|document|summary|activity}.md`.
   - Ground every claim in a wiki page or explicitly flag it as original synthesis.
   - Follow style from `pages/mem-claude.md` §4 (Preferences).

3. **Refine**
   - Check against preferences (concise, specific, actionable, active voice).
   - Ensure every wiki claim carries a `[[wiki/concepts/...]]` reference.
   - Add visuals/diagrams where they clarify — fenced ```mermaid``` blocks render natively in Logseq.

4. **Save**
   - Filename: `pages/output-{type}-YYYY-MM-DD-{project}-{slug}.md`
   - First block:
     ```
     title:: output/{type}/YYYY-MM-DD-{project}-{slug}
     type:: report | presentation | template | document | summary | visual
     date:: YYYY-MM-DD
     status:: draft
     sources:: [[wiki/concepts/...]]
     related_outputs::
     tags::
     ```

5. **Link back**
   - Update the relevant wiki pages so they point forward to this output too.

6. **Log**
   - Append to `log.md` and a block to today's `journals/yyyy_MM_dd.md`.

## Output
Report: artifact saved (path), key claims grounded, confidence level, known gaps.
