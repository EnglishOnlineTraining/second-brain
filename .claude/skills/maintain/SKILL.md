---
name: maintain
description: Health-check the second-brain Logseq graph — find orphan pages, stale stubs, broken or weak references, contradiction gaps, dangling outputs, near-duplicate pages, and a stale wiki index. Use whenever Shaun says "/maintain lint", "clean up the vault", "run maintenance", or on scheduled weekly maintenance.
---

# /maintain — Health Check, Prune, Dedupe, Improve Links

**Trigger:** User requests lint, or scheduled weekly maintenance.

**Usage**
```
/maintain lint
```

## Checks (in order)

| Check | What to Find | Severity | Action |
|-------|-------------|----------|--------|
| Orphans | Pages under `pages/wiki-*` with zero Linked References | warn | Suggest 2-3 pages to link from |
| Stub decay | `status:: stub` older than 30 days | warn | Suggest expand/merge/delete |
| Broken references | `[[references]]` to pages that stay empty stubs long-term | fix | Auto-fix: unlink, or create a real stub page if referenced ≥3 times |
| Contradiction orphans | A `## Contradictions` block with only one side documented | warn | Flag for human |
| Source drift | Claims without a `sources::` attribution | critical | Flag for human |
| Dangling outputs | `pages/output-*` whose source wiki page is gone | fix | Set `status:: archived` |
| Duplicates | >70% content overlap or near-identical `title::` | warn | Suggest merge, ask human before doing |
| Index freshness | `pages/wiki-index.md` missing pages that exist under `pages/wiki-*` | fix | Regenerate the missing entries |

Logseq's own **Linked References** / **Unlinked References** panel at the
bottom of any page is the fastest manual spot-check for the Orphans and
Broken-references rows — this skill reproduces that programmatically across
the whole graph.

## Output
Report: a markdown table of Check | Found | Auto-fixed | Needs Human. Then append the same summary to `log.md`.
