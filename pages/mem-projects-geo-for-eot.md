title:: mem/projects/geo-for-eot
type:: project
status:: active
tags:: geo, seo, ai-search, englishonline-training
created:: 2026-08-23
updated:: 2026-10-21

- ## Brief
	- Apply GEO/AI-search content-optimization practice (see [[wiki/concepts/geo]]) to englishonline.training / the `vocab-games` repo — check the real site against the structural/formatting checklist from that ingest, and fix what's worth fixing.
- ## Status
	- Audit of the activities host (`vocab-games`) done 2026-10-21: see [[mem/projects/geo-for-eot/audit-2026-10-21]]. Structure is in good shape; six small copy/style gaps listed there. WordPress main site not re-audited here (Tier 8 crawl in the repo's `docs/seo-backlog.md` covers it).
- ## Key Questions
	- Are page titles, H1s, and meta descriptions tightly aligned site-wide, the way the GEO source recommends?
	- Are the "Auf einen Blick" Quick Overview boxes and `themen/` topic-page prose actually snippable (concise, self-contained 1–2 sentence answers), or written as longer paragraphs?
	- How complete is schema.org/JSON-LD coverage across the ~183 exercise pages, hubs, and `themen/` pages — is `FAQPage` markup (currently only on `msa-activities.html`/`abitur-mediation.html`) worth extending anywhere else?
	- Any of the named anti-patterns present — content hidden in tabs/accordions, key info only in a PDF or only in an image without alt text, decorative punctuation, unanchored buzzwords?
- ## Decisions
	- **2026-08-23:** Scoped this as its own project rather than folding it into [[mem/projects/ai-activities-website]] — that project is about *building* AI-generated activities, this one is about the *existing* site's discoverability to AI search assistants. Related but distinct.
- ## Blockers
	- None. Gap 5 on the audit page (stale `Speakable` lines in the repo backlog, possible `speakable` node on WordPress `/about/`) needs Shaun.
- ## Next Actions
	- DONE Audit `vocab-games`/englishonline.training against the [[wiki/concepts/geo]] checklist (title/H1/description alignment, snippability of Quick Overview boxes and `themen/` prose, schema.org/FAQPage coverage, anti-pattern check) — added 2026-08-23, done 2026-10-21 for the activities host: [[mem/projects/geo-for-eot/audit-2026-10-21]]
	- TODO Shaun to triage the audit's six gaps (long meta descriptions, emoji H1s vs VOICE.md, long `themen/` openers, symbols, stale Speakable lines, 4 pages without overview box).
- ## Related
	- [[mem/projects/geo-for-eot/audit-2026-10-21]] — the audit result, pass/fail per checklist item
	- [[wiki/concepts/geo]] — the source concept/checklist this project applies
	- [[wiki/articles/2026-08-23-ai-search-content-optimization-summary]] — the ingest this grew out of
	- [[mem/projects/ai-activities-website]] — sibling project, different angle (building activities vs. surfacing the existing site)
