# System Log

> Reverse-chronological audit trail of all operations. Append new entries at the TOP.

## 2026-08-23 08:00
- **Operation:** ingest
- **Source:** `raw/articles/2026-08-23-ai-search-content-optimization.md` (pasted directly by Shaun — appears to be a Microsoft Advertising blog post on GEO/AI search content optimization)
- **Pages created:** [[wiki/concepts/geo]], [[wiki/articles/2026-08-23-ai-search-content-optimization-summary]]
- **Pages updated:** [[wiki/index]]
- **Evidence quality:** moderate for the one cited statistic (357% YoY AI-referral growth, TechCrunch/SimilarWeb, not independently re-verified); weak/anecdotal for the prescriptive formatting/structure advice (no citations backing individual recommendations, and the source is a vendor blog promoting its own webinar)
- **Notes:** Outside the vault's two declared focus areas (not learning-science, not edtech) — flagged honestly rather than force-fit. Kept because it's directly, concretely actionable for englishonline.training's real SEO/schema.org infrastructure (see `vocab-games` CLAUDE.md §5g) — the source's checklist doubles as a ready-made audit list for that site. Cross-linked to [[wiki/concepts/graft]] (both are about chunking content for machine consumption, different AI consumers).

## 2026-08-23 07:00
- **Operation:** manage (hands-on test, follow-up to the Graft ingest)
- **Notes:** Installed Graft (`npm install -g @nanonets/graft`) and ran its free deterministic tier against `vocab-games`. Worked and was fast (1.3s, 217 nodes/420 edges, $0). Found a real, independently-discovered limitation not in the source material: it can't see the inline `<script>` logic inside `vocab-games`'s 220+ HTML pages, so its call-graph output (`graft callers checkDropdowns` → 1 caller found, actual ≈150+) would mislead anyone trusting it there. Reverted the incidental `.gitignore`/`graft/` changes left in `vocab-games` — not adopted as an ongoing tool for that repo. [[wiki/concepts/graft]] updated (`stub` → `draft`) with the hands-on findings.

## 2026-08-23 06:00
- **Operation:** ingest
- **Source:** `raw/articles/2026-08-23-graft-readme.md` (https://github.com/NanoNets/Graft)
- **Pages created:** [[wiki/concepts/graft]], [[wiki/articles/2026-08-23-graft-readme-summary]]
- **Pages updated:** [[wiki/index]]
- **Evidence quality:** weak-to-moderate — all benchmark figures are vendor-self-reported (no independent replication in source); descriptive/architectural claims are well-grounded as primary source
- **Notes:** Off-topic-ish source (AI coding-agent dev tooling, not learning science/edtech) — ingested as requested. Relevance flagged honestly in both pages rather than force-fit into the focus areas; no `wiki/people/*` page created since no named individuals were credited, only the org (NanoNets).

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
