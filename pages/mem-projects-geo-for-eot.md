title:: mem/projects/geo-for-eot
type:: project
status:: active
tags:: geo, seo, ai-search, englishonline-training
created:: 2026-08-23
updated:: 2026-08-23

- ## Brief
	- Apply GEO/AI-search content-optimization practice (see [[wiki/concepts/geo]]) to englishonline.training / the `vocab-games` repo — check the real site against the structural/formatting checklist from that ingest, and fix what's worth fixing.
- ## Status
	- Just started — backlog has one item, no audit run yet.
- ## Key Questions
	- Are page titles, H1s, and meta descriptions tightly aligned site-wide, the way the GEO source recommends?
	- Are the "Auf einen Blick" Quick Overview boxes and `themen/` topic-page prose actually snippable (concise, self-contained 1–2 sentence answers), or written as longer paragraphs?
	- How complete is schema.org/JSON-LD coverage across the ~183 exercise pages, hubs, and `themen/` pages — is `FAQPage` markup (currently only on `msa-activities.html`/`abitur-mediation.html`) worth extending anywhere else?
	- Any of the named anti-patterns present — content hidden in tabs/accordions, key info only in a PDF or only in an image without alt text, decorative punctuation, unanchored buzzwords?
- ## Decisions
	- **2026-08-23:** Scoped this as its own project rather than folding it into [[mem/projects/ai-activities-website]] — that project is about *building* AI-generated activities, this one is about the *existing* site's discoverability to AI search assistants. Related but distinct.
- ## Blockers
	- None yet — audit hasn't started.
- ## Next Actions
	- TODO Audit `vocab-games`/englishonline.training against the [[wiki/concepts/geo]] checklist (title/H1/description alignment, snippability of Quick Overview boxes and `themen/` prose, schema.org/FAQPage coverage, anti-pattern check) — added to backlog 2026-08-23, not yet started.
- ## Related
	- [[wiki/concepts/geo]] — the source concept/checklist this project applies
	- [[wiki/articles/2026-08-23-ai-search-content-optimization-summary]] — the ingest this grew out of
	- [[mem/projects/ai-activities-website]] — sibling project, different angle (building activities vs. surfacing the existing site)
