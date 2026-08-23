# /maintain

Prune stale content, deduplicate, improve links, and run health checks.

## Usage
```
/maintain lint
/maintain prune --older-than 90d --status stub
/maintain dedupe --similarity 0.7
/maintain links --orphans --broken --weak
```

## Workflow

1. **Lint**
   - Orphaned pages: zero incoming links (exclude index, templates).
   - Stub decay: `status: stub` older than 30 days.
   - Broken links: wikilinks to non-existent files.
   - Contradiction orphans: `## Contradictions` with only one side.
   - Source drift: claims without source attribution.
   - Dangling outputs: output files where source wiki pages no longer exist.
   - Report as markdown table: Check | Found | Auto-fixed | Needs Human.

2. **Prune**
   - Identify pages that are stubs, unlinked, and old.
   - Suggest: expand, merge into related page, or archive.
   - **Never delete without human approval.** Mark as `status: archived` instead.

3. **Dedupe**
   - Find pages with >70% content overlap or very similar titles.
   - Suggest merge target and which page to keep.
   - **Never merge without human approval.**

4. **Improve Links**
   - Find pages that mention concepts but don't link them.
   - Suggest 2-3 new links per page.
   - Identify "bridge" opportunities: two clusters of knowledge that aren't connected yet.

5. **Update Index**
   - Regenerate `wiki/index.md` with current structure.
   - Update `mem/claude.md` if directory rules changed.

6. **Log**
   - Append to `log.md`.

## Output
Report: lint results, prune suggestions, dedupe candidates, link improvements made/suggested.
