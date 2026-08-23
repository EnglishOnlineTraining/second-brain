title:: wiki/concepts/fsrs
type:: concept
created:: 2026-08-23
updated:: 2026-08-23
status:: stub
category:: learning-science
sources:: [[raw/articles/2026-08-23-fsrs4anki-readme]]
related:: [[wiki/people/jarrett-ye]], [[wiki/people/damien-elmes]]
tags:: spaced-repetition, algorithm, anki

- ## Definition
	- FSRS (Free Spaced Repetition Scheduler) is a data-driven, open-source spaced-repetition scheduling algorithm — an alternative to the older SM-2 algorithm that Anki/SuperMemo historically used. It has two parts: a **scheduler** that decides when to show a card next, and an **optimizer** that uses machine learning on a learner's own review history to fit parameters to their personal memory patterns, rather than using one fixed formula for everyone.
- ## Key Insights
	- It explicitly replaces SM-2's "Ease Factor" mechanism — when FSRS is enabled in Anki, Ease Factor and the New Interval setting stop being relevant, implying a materially different underlying model, not just a tuned version of SM-2.
	- The model is personalized per-learner via the optimizer fitting to individual review history, rather than a global fixed schedule — this is the core differentiator from classic spacing algorithms.
	- It's built and maintained by the open-source community around MaiMemo/Anki (see [[wiki/people/jarrett-ye]], [[wiki/people/damien-elmes]]), not a single commercial vendor.
- ## In Practice
	- Ships integrated into Anki 23.10+; older Anki versions need manual setup via a separate tutorial.
	- Not all Anki add-ons are compatible — anything that also manipulates card intervals directly (Delay Siblings, Auto Ease Factor, etc.) conflicts with FSRS's own interval logic.
	- Explicitly **not** designed for incremental-reading workflows — a specific, named limitation from the source, not an inference.
- ## Connections
	- [[wiki/people/jarrett-ye]] — FSRS research engineer, primary author of this implementation
	- [[wiki/people/damien-elmes]] — Anki's founder, provided technical support for the integration
	- [[wiki/concepts/spaced-repetition]] — the broader concept this algorithm implements (page not yet created — flagged in wiki/index)
- ## Contradictions
	- None found yet — only one source ingested so far.
- ## Open Questions
	- The specific memory-factor model (widely known elsewhere as difficulty/stability/retrievability, sometimes called "DSR") was **not** detailed in the ingested README — this page deliberately does not assert those mechanics as sourced, pending a better primary source (the linked academic papers, not yet ingested).
	- Two academic papers are cited (KDD, TKDE) but their actual findings/benchmarks were not in the ingested text — worth a follow-up `/ingest` once accessible.
	- No comparative benchmark data (FSRS vs. SM-2 retention/efficiency) was found in this source — can't yet back the "FSRS is better" claim that's common folklore around it; flagging rather than asserting.
