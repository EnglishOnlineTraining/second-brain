# /manage

Log decisions, link them to context, and track progress against goals.

## Usage
```
/manage decision "<decision text>" --context "<wiki pages or sources>" --goal "<goal name>"
/manage track --goal "<goal name>" --progress "<update>"
/manage link --from "<page>" --to "<page>" --reason "<why>"
/manage project --name "<project>" --status active|paused|complete
```

## Workflow

1. **Decision Logging**
   - Create `ctx/sessions/YYYY-MM-DD-{decision-slug}.md`:
     ```yaml
     ---
     type: decision
     date: YYYY-MM-DD
     context:
       - "[[wiki/concepts/...]]"
       - "[[raw/...]]"
     goal: "[[mem/goals/...]]"
     status: provisional | confirmed | reversed
     ---
     ```
   - Body: Decision made → Alternatives considered → Why this one → What would change my mind → Review date

2. **Progress Tracking**
   - Read `mem/goals/{goal}.md`.
   - Append progress update with date, metric, and blockers.
   - If goal is complete, mark status and write retrospective in `mem/history/`.

3. **Context Linking**
   - When two wiki pages should be connected but aren't, add bidirectional links.
   - Document the relationship: "X contradicts Y on Z" or "X is a prerequisite for Y."
   - Save linking rationale in `ctx/sessions/` if non-obvious.

4. **Project Management**
   - Create/update `mem/projects/{project}.md` with status, key decisions, blockers, next actions.
   - Link to relevant wiki pages, outputs, and decisions.

## Output
Report: decisions logged, goals updated, links added, project status.
