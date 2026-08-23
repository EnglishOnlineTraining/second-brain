---
name: manage
description: Log a decision to today's journal, update a goal's progress, or update a project's status in the second-brain Logseq graph. Use whenever Shaun makes a decision he wants recorded, gives a progress update against a goal, or wants a project's status/blockers/next-actions updated.
---

# /manage — Log Decisions, Track Goals, Link Context

**Trigger:** User makes a decision, updates a goal, or wants to track progress.

**Usage**
```
/manage decision "..."
/manage goal "<goal-slug>" progress "..."
/manage project "<project-slug>" status "..."
```

## Workflow

1. **Decision logging**
   - Append a block to **today's journal** (`journals/yyyy_MM_dd.md`, create it if it doesn't exist yet) — decisions do NOT get their own page in this graph.
   - Use the shape in `pages/templates-ctx-session.md`: Objective → Decision → Alternatives → Why this one → What would change my mind.
   - Link to relevant `[[wiki/concepts/...]]` and `[[mem/goals/...]]`/`[[mem/projects/...]]` pages inline.

2. **Goal tracking**
   - Read `pages/mem-goals-{goal}.md` (or `pages/ctx-goals-{goal}.md` for a lighter-weight working goal not yet promoted to `mem/`).
   - Append a Progress Log bullet: date, what happened, metric.
   - If complete: set `status:: complete` and write a retrospective block in `pages/mem-history-{topic}.md`.

3. **Project updates**
   - Update `pages/mem-projects-{project}.md`: status, decisions (link to the journal block), blockers, next actions.
   - Use Logseq's native `TODO` / `DOING` / `DONE` keywords for next actions, not markdown checkboxes.

4. **Log**
   - Append to `log.md`.
