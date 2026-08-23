# /write

Retrieve relevant context, draft an artifact, refine it, and save to output/.

## Usage
```
/write <artifact-type> <topic-or-goal> [--draft-only]
/write report "adaptive learning activity frameworks"
/write presentation "self-organized learning models"
/write template "spaced-repetition-quiz-activity"
/write document "AI activity generation pipeline"
```

## Workflow

1. **Retrieve context**
   - Search `wiki/` for relevant concepts, people, literature, permanent-notes.
   - Read the most relevant pages fully.
   - Note contradictions, gaps, or weak evidence that affects the artifact.

2. **Draft**
   - Choose the right output template from `templates/output/`.
   - Draft grounded in retrieved wiki content. Every claim must trace to a wiki page or be flagged as original synthesis.
   - For reports: structure with TL;DR → Key Findings → Deep Dive → Connections → Open Questions.
   - For presentations: story arc → one idea per section → visual placeholders.
   - For templates: reusable structure with variables, examples, and usage instructions.
   - For documents: formal structure with references, versioning, and approval workflow.

3. **Refine**
   - Check against `mem/claude.md` style preferences.
   - Ensure all wiki claims are linked: `[[wiki/concepts/...]]`.
   - Add visuals/diagrams where they clarify (Mermaid, ASCII, or placeholder).
   - Self-critique: what would a skeptical expert object to?

4. **Save**
   - Save to `output/{type}/YYYY-MM-DD-{project}-{slug}.md`
   - Add output frontmatter:
     ```yaml
     ---
     type: report | presentation | template | document | summary | visual
     date: YYYY-MM-DD
     status: draft | review | published | archived
     sources:
       - "[[wiki/concepts/...]]"
       - "[[wiki/literature/...]]"
     related_outputs:
       - "[[output/...]]"
     tags: []
     ---
     ```

5. **Log & Link**
   - Append to `log.md`.
   - Add the output to `wiki/index.md` outputs section.
   - If the output resolves or advances a goal, update `mem/goals/`.

## Output
Report: artifact saved, key claims grounded in wiki pages, confidence level, known gaps.
