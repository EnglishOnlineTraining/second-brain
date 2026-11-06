---
type: source
date: 2026-11-02
origin: "X article by Nicholas Dulait (@NicholasDulait), 'Claude SEO Second Brain: The Complete Guide', pasted into chat by Shaun on 2026-11-02 (no URL given)"
media: article
tags: [claude-code, memory, seo, hooks]
status: extracted
---

Note: condensed copy of the pasted article, every point kept. The author's promotional lines for chatseo.app (an ad, not part of the method) were dropped.

# Claude SEO Second Brain: The Complete Guide

I run all of our SEO out of this setup. Here it is, file by file, for free.
My Claude Code knows our site through a 128-line map, 17 skills and 171 memory files it mostly wrote itself.

Every session you start, Claude forgets your SEO. Every Claude Code session starts with a fresh context window, and every correction you only typed in chat disappears when the session ends.

Claude Code has four memory layers. Most SEOs use one, stuff it until Claude stops listening, and decide "AI can't do SEO."

## The Short Answer
An SEO second brain in Claude Code is four layers, each loading at a different moment:
1. CLAUDE.md, the map. You write it. Loads every session. Your site, your audience, your money pages, the rules Claude needs every single time.
2. .claude/rules/, the reflexes. You write them. Load only when Claude touches matching files.
3. Skills, the playbooks. You write them. Load only when invoked or relevant. Content brief, page refresh, monthly report.
4. Auto memory, the diary. Claude writes it. Loads every session (first 200 lines or 25KB).

Golden rule: put each piece of SEO knowledge in the layer that loads only when it's needed.

## What you need
Claude Code; one folder per site of plain .md files; your Search Console; 10 minutes. No installs, plugins or database.

## Two myths
Myth 1: "CLAUDE.md is the system prompt, so Claude obeys it." The docs say CLAUDE.md content is delivered as a user message after the system prompt. Claude tries to follow it, with no guarantee of strict compliance, especially for vague rules.
Myth 2: "Write 'never touch robots.txt' and you're protected." Anthropic says Claude treats memory files "as context, not enforced configuration." If something must never happen, use a PreToolUse hook.

## The skeleton
```
my-site-seo/
├── CLAUDE.md            # Layer 1: the map (keep under 200 lines)
├── CLAUDE.local.md      # private notes (gitignore it)
├── decisions.md         # every SEO call you made, and why
├── strategy/            # audience, positioning, competitors
├── keywords/            # one cluster per file
├── pages/               # one money page per file: URL, target query, status
├── briefs/              # content briefs in progress
├── reports/             # monthly Search Console reviews
└── .claude/
    ├── rules/           # Layer 2
    │   ├── briefs.md    # paths: briefs/**
    │   └── pages.md     # paths: pages/**
    └── skills/
        └── page-refresh/SKILL.md
```
One topic per file, lowercase, hyphens.

## Layer 1: CLAUDE.md under 200 lines
Docs target under 200 lines per CLAUDE.md; longer files "consume more context and reduce adherence." Theirs is 128 lines.
Example sections: The site (sells, reader, money pages — never change their URLs); Where things live; How to answer (real data before opinions, ask for Search Console numbers, quote the file used, say if no file covers it); Always in focus (@strategy/now.md).
Tricks: block-level HTML comments are stripped before loading (free notes for humans). @imports organise but don't reduce context cost — import only what must always be in focus. Backticks around a path turn an import off. /init drafts a starter CLAUDE.md. CLAUDE.local.md is personal; ~/.claude/CLAUDE.md is global.

## Layer 2: .claude/rules/ with paths:
Markdown files with a `paths:` frontmatter field load only when Claude reads or edits matching files. Rules without paths load at launch like CLAUDE.md.
pages.md (paths: pages/**): never change a URL with clicks in the last 90 days; one target query per page, check keywords/ first; every edit gets a dated line in decisions.md.
briefs.md (paths: briefs/**): start from the top 10 results, not memory; say what the page adds that the top 10 don't — no answer, no brief; never invent a statistic.

## Layer 3: Skills
CLAUDE.md is for facts; procedures belong in skills, which load only when invoked or judged relevant. They run 17.
page-refresh skill: 1) pull last 90 days vs previous 90 from Search Console for the page; 2) list queries that lost clicks and ones with impressions but no clicks; 3) read pages/<page>.md and matching rules first; 4) propose edits — new sections for missing queries, title/meta only if CTR is below the site average for that position, never touch the URL; 5) log change and date in decisions.md.

## Layer 4: Auto memory
Notes Claude writes from corrections and preferences; per repository; plain Markdown. "remember X" saves to auto memory; "add this to CLAUDE.md" goes to the map; /memory lists and opens files. Theirs: 171 files, 63 of them corrections.
Where it broke: auto memory loads the first 200 lines or 25KB of its index. Their index grew to 213 lines / 32.5KB, so 52 lines were silently cut every session; only a warning line appended to the loaded index. Lesson: one line per index entry, detail in the topic file, check index size monthly.
A real "never" is a PreToolUse hook (theirs stops several sessions driving one Chrome at once). For SEO: a hook on Edit|Write running .claude/hooks/protect.sh that exits 2 when the path contains robots.txt. Tested: the write was blocked.

## One-prompt setup (summary)
Create the folders; a CLAUDE.md under 200 lines; rules/pages.md and rules/briefs.md with paths; a page-refresh skill; decisions.md and strategy/now.md imported from CLAUDE.md; CLAUDE.local.md gitignored; then ask 5 questions to fill CLAUDE.md, inventing nothing. Run /context to check CLAUDE.md appears under "Memory files".

## Load order
1. At launch: every CLAUDE.md and CLAUDE.local.md from the folder and every folder above, concatenated.
2. Also at launch: rules without paths, plus the auto memory index.
3. On demand: subfolder CLAUDE.md files and path-scoped rules, the first time Claude touches a matching file.
4. After /compact: root CLAUDE.md is re-read from disk; rules typed only in chat are gone.

## Five commands
/init; /memory; /context; /doctor prompt-audit (finds outdated or contradicting instructions; v2.1.283+); "remember …".

## Pitfalls
Huge CLAUDE.md; whole keyword list @-imported; two files disagreeing on a page's target query (Claude "may pick one arbitrarily"); "never noindex X" only in CLAUDE.md (use a hook); a rule typed only in chat (gone after /compact); auto memory index past 200 lines.

## 60-second audit
1. Does /context list your CLAUDE.md under Memory files? 2. Under 200 lines? 3. Auto memory on and its index under 200 lines? 4. Is your most important "never" a hook? 5. One file and one target query per money page? Three or more "no" = a notes folder, not a brain.

## Caveat
A sample of one company. If you touch your site once a month, a 30-line CLAUDE.md is enough; the four layers pay off with daily use. What generalises is the placement rule, not their exact files.
