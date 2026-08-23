---
name: review
description: Run a weekly or monthly review of the second-brain graph — summarize what was ingested/written/decided, reflect on what worked, and update mem/preferences, mem/goals, or mem/claude if the system should change. Use whenever Shaun says "/review weekly", "/review monthly", or asks for a review/retrospective of recent second-brain activity.
---

# /review — Summarize, Reflect, Update System

**Trigger:** User requests weekly or monthly review.

**Usage**
```
/review weekly
/review monthly
```

## Workflow

1. **Read `log.md`** for the review period, plus the `journals/*.md` files covering those dates.
2. **Count:** sources ingested, pages created/updated, outputs generated.
3. **Identify:** top 3-5 most important new insights.
4. **Reflect:** What worked? What didn't? What should change?
5. **Update system:**
   - Preferences evolved → update `pages/mem-preferences-style-and-workflow.md` and `pages/mem-claude.md` §4
   - Goals shifted → update `pages/mem-goals-*.md`
   - Major insight changes the system itself → update `pages/mem-history-*.md`
6. **Write the review:** Save to `pages/mem-history-YYYY-MM-DD-{weekly|monthly}-review.md`.
7. **Log:** Append to `log.md`.
