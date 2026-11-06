title:: wiki/concepts/claude-code-memory-layers
type:: concept
created:: 2026-11-02
updated:: 2026-11-02
status:: draft
category:: ai
sources:: [[raw/articles/2026-11-02-claude-seo-second-brain-complete-guide]]
related:: [[wiki/concepts/graft]], [[wiki/concepts/geo]], [[mem/projects/geo-for-eot]]
tags:: claude-code, memory, seo, hooks

- ## Definition
	- Claude Code starts every session with an empty context window, so durable knowledge has to live in files that Claude loads at the right moment. There are four layers, each loading at a different time: **CLAUDE.md** (the map, you write it, loads every session), **`.claude/rules/` with `paths:`** (reflexes, load only when Claude touches matching files), **skills** (playbooks, load when invoked or judged relevant) and **auto memory** (the diary, Claude writes it, its index loads every session). The placement rule: put each piece of knowledge in the layer that loads only when it is needed. Applied to SEO in [[wiki/articles/2026-11-02-claude-seo-second-brain-summary]].
- ## Key Insights
	- **Facts go in CLAUDE.md, procedures go in skills.** Docs target under 200 lines per CLAUDE.md; longer files "consume more context and reduce adherence". The source's own map is 128 lines, with 17 skills.
	- **Auto memory has a hard load limit: the first 200 lines or 25KB of its index.** The source's index grew to 213 lines / 32.5KB, so 52 lines were silently cut every session; the only sign was a warning line appended to the loaded index. Fix: one line per index entry, detail in the topic file, check index size monthly.
	- **Memory files are context, not enforcement.** CLAUDE.md arrives as a user message after the system prompt; Claude tries to follow it, with no guarantee, especially for vague rules. A real "never" is a `PreToolUse` hook that exits 2 (the source's example: block Edit|Write when the path contains `robots.txt`; tested, the write was blocked).
	- **Load order matters.** At launch: all CLAUDE.md files up the tree, rules without `paths:`, the auto memory index. On demand: subfolder CLAUDE.md and path-scoped rules. After `/compact` the root CLAUDE.md is re-read from disk; rules typed only in chat are gone.
	- **Conflicts are resolved arbitrarily.** Two files disagreeing (e.g. on a page's target query) means Claude "may pick one arbitrarily". One file and one target query per money page.
	- **@imports organise but do not save context.** Import only what must always be in focus.
	- **60-second audit (the source's):** (1) does `/context` list CLAUDE.md under Memory files? (2) under 200 lines? (3) auto memory on, index under 200 lines? (4) is the most important "never" a hook? (5) one file and one target query per money page? Three or more "no" = a notes folder, not a brain.
- ## In Practice
	- Same domain as [[wiki/concepts/geo]]: both are about making a site legible to AI, but this one is about the operator's side, how Claude Code is set up to work on the site. [[wiki/concepts/graft]] attacks the same "agents re-onboard every session" problem from the tooling side.
	- **Relevance to Shaun's setup:** englishonline.training runs its SEO from the `vocab-games` repo with a CLAUDE.md plus `docs/claude-reference/`, skills and an auto-memory index, which is the same four-layer shape. Two audit points are worth checking there; both are tracked as `LATER` items in [[mem/projects/geo-for-eot]] and are **not changes**:
		- the auto-memory index size against the 200-line / 25KB limit (silent truncation), and the same line-count check for CLAUDE.md;
		- whether the live-page "nevers" (for example "never edit live WordPress without a go-ahead", "never change a money-page URL") are only prose in CLAUDE.md or are backed by a hook.
	- Note on fit: the source is a daily-use SEO operation. It says itself that a site touched once a month needs only a ~30-line CLAUDE.md.
- ## Connections
	- [[wiki/concepts/graft]] — persistent context for coding agents; same problem, different mechanism
	- [[wiki/concepts/geo]] — the site-side AI-search checklist this operator-side setup supports
	- [[mem/projects/geo-for-eot]] — project that carries the LATER audit items
- ## Contradictions
	- None found yet, single source. The "CLAUDE.md is not enforced" claim agrees with the Anthropic docs the source quotes, but the docs were not re-read in this ingest.
- ## Verification (2026-11-02, against code.claude.com/docs/en/memory and /hooks)
	- **Confirmed:** CLAUDE.md under 200 lines; CLAUDE.md delivered as a user message, "no guarantee of strict compliance"; memory is "context, not enforced configuration", use a `PreToolUse` hook to block; auto-memory index loads first 200 lines or 25KB; `paths:` rules; HTML block comments stripped; backticks stop an `@import`; `CLAUDE.local.md`; conflicting instructions "may pick one arbitrarily"; root CLAUDE.md re-read after `/compact`; `/context` lists Memory files; hook exit 2 blocks the call.
	- **Confirmed by third-party posts only:** `/doctor prompt-audit` (added in 2.1.283, 2026-09-25; the docs now describe `/doctor` auditing CLAUDE.md, rules, skills).
	- **Not confirmed / softened:** the "warning line appended to the loaded index" detail. The docs say Claude Code reminds Claude to shorten the file when it is near a limit after a write; the silent cut itself is consistent with "content beyond that threshold is not loaded".
	- **Caveats the source omits:** a hook that crashes, times out or exits with anything but 2 does not block (unless `onFailure: block`, v2.1.295+). An `Edit|Write` matcher does not see changes made through Bash (`sed -i`, redirects), so the `robots.txt` example needs a Bash rule too, and the docs prefer permission rules for hard denies.
	- **Checked in vocab-games (read-only, 2026-11-02):** auto-memory `MEMORY.md` is 14 lines / 1.8KB (far under the limit). Root `CLAUDE.md` is 219 lines / 14KB (over the 200-line target). No hooks found in the project `.claude/settings*.json`. Details feed the two LATER items in [[mem/projects/geo-for-eot]].
- ## Open Questions
	- The author's own figures (128 lines, 17 skills, 171 files, 213-line index) remain self-reported and unchecked.
