# /review

Summarize what was learned, reflect on the system, and update identity/preferences.

## Usage
```
/review weekly
/review monthly
/review project --name "<project>"
```

## Workflow

1. **Summarize**
   - Read `log.md` for the review period.
   - Count: sources ingested, wiki pages created/updated, outputs generated, decisions made.
   - Identify top 3-5 most important new insights.

2. **Reflect**
   - What worked well? (e.g., cross-linking improved, output quality up)
   - What didn't work? (e.g., too many stubs, shallow captures, missed connections)
   - What should change? (e.g., ingest more literature, write more permanent notes, review more often)

3. **Update System**
   - If style preferences evolved, update `mem/preferences/` and `mem/claude.md` §4.
   - If goals shifted, update `mem/goals/`.
   - If a major insight changes how the system should work, update `mem/history/` and `mem/claude.md`.

4. **Write Review Document**
   - Save to `mem/history/YYYY-MM-DD-{weekly|monthly}-review.md`:
     ```yaml
     ---
     type: review
     period: YYYY-MM-DD to YYYY-MM-DD
     sources_ingested: N
     pages_created: N
     pages_updated: N
     outputs_generated: N
     ---
     ```
   - Body: Summary → Reflections → System Changes → Next Period Priorities

5. **Log**
   - Append to `log.md`.

## Output
Report: review saved, system updates made, next period priorities.
