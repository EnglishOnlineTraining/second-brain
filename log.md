# System Log

> Reverse-chronological audit trail of all operations. Append new entries at the TOP.

## 2026-08-23 05:00
- **Operation:** ingest
- **Source:** `raw/articles/2026-08-23-fsrs4anki-readme.md` (https://raw.githubusercontent.com/open-spaced-repetition/fsrs4anki/main/README.md)
- **Pages created:** [[wiki/concepts/fsrs]], [[wiki/people/jarrett-ye]], [[wiki/people/damien-elmes]], [[wiki/articles/2026-08-23-fsrs4anki-readme-summary]]
- **Pages updated:** [[wiki/index]]
- **Evidence quality:** moderate for descriptive claims (primary-source README); weak for performance claims (no benchmark data in source — flagged, not asserted)
- **Notes:** First live test of the `/ingest` pipeline post-Logseq-migration. All new pages carry `title::` properties, are cross-linked (≥2 outgoing references each), and this is a real end-to-end run, not a dry run.

## 2026-08-23 04:15
- **Operation:** restructure
- **Notes:** Rebuilt as a native Logseq graph (`journals/`, `pages/`, `logseq/config.edn`, `assets/`), separate from any other project. Moved `wiki/`, `mem/`, `ctx/`, `output/`, `templates/` content into flat `pages/*.md` files with namespaced `title::` properties. `raw/` kept outside the graph, unchanged. Rewrote `CLAUDE_CODE_INSTRUCTIONS.md`, `CLAUDE.md`, `README.md` for Logseq's property/block conventions. Converted the five skills to proper `.claude/skills/<name>/SKILL.md` folders (with frontmatter) so Claude Code actually discovers them. See [[mem/history/system-evolution]] and today's journal entry for the full decision log. Ready for first ingest.

## 2026-08-22 11:00
- **Operation:** init
- **Notes:** Second Brain v1.0 initialized. Directory structure, skills, templates, and starter files created. Focus areas: self-organized learning and AI-optimized activities website. Ready for first ingest.
