title:: wiki/articles/2026-11-02-claude-seo-second-brain-summary
type:: article-summary
created:: 2026-11-02
updated:: 2026-11-02
status:: draft
source:: [[raw/articles/2026-11-02-claude-seo-second-brain-complete-guide]]
concepts:: [[wiki/concepts/claude-code-memory-layers]], [[wiki/concepts/geo]]
people::
tags:: claude-code, seo, memory, hooks

- ## One-Line Essence
	- Nicholas Dulait's X article ("Claude SEO Second Brain: The Complete Guide", 2026-11) argues that SEO knowledge belongs in four Claude Code memory layers, each placed where it loads only when needed, and that anything that must never happen needs a hook, not a CLAUDE.md line.
- ## Key Arguments
	- 1. Four layers: CLAUDE.md (map, under 200 lines), path-scoped `.claude/rules/` (reflexes), skills (playbooks, e.g. a `page-refresh` procedure), auto memory (diary written by Claude).
	- 2. Auto memory loads only the first 200 lines or 25KB of its index; the author's index hit 213 lines / 32.5KB and 52 lines were silently dropped each session. One line per entry, check monthly.
	- 3. CLAUDE.md is "context, not enforced configuration". The only real "never" is a `PreToolUse` hook (example: exit 2 on Edit|Write of `robots.txt`).
	- 4. A 60-second, five-question audit: `/context` shows CLAUDE.md, under 200 lines, auto-memory index under 200 lines, key "never" is a hook, one file and one target query per money page.
	- 5. Pitfalls: huge CLAUDE.md, whole keyword list @-imported, conflicting files, rules typed only in chat (lost after `/compact`).
- ## Concepts Introduced
	- [[wiki/concepts/claude-code-memory-layers]] — the four layers, limits, hooks, audit
- ## Evidence Quality
	- **Anecdotal-to-weak.** One company's own setup, self-reported numbers, and the article carries ads for the author's product (dropped from the raw copy). The mechanics it describes (load order, hooks) quote Anthropic's docs and are plausible, but were checked against the Claude Code docs on 2026-11-02: all core claims hold, see Verification on [[wiki/concepts/claude-code-memory-layers]]. The author's own numbers and the sales framing remain unchecked. The author states the caveat: what generalises is the placement rule, not the exact files.
- ## My Take
	- *RESERVED FOR HUMAN CURATOR.*
- ## Follow-Up Questions
		- Is the `vocab-games` auto-memory index near the limit? See the LATER items in [[mem/projects/geo-for-eot]].
