title:: wiki/articles/2026-08-23-fsrs4anki-readme-summary
type:: article-summary
created:: 2026-08-23
updated:: 2026-08-23
status:: draft
source:: [[raw/articles/2026-08-23-fsrs4anki-readme]]
concepts:: [[wiki/concepts/fsrs]]
people:: [[wiki/people/jarrett-ye]], [[wiki/people/damien-elmes]]
tags:: spaced-repetition, anki

- ## One-Line Essence
	- FSRS is an open-source, machine-learning-based spaced-repetition scheduler for Anki that replaces SM-2's fixed ease-factor formula with a model personalized to each learner's own review history.
- ## Key Arguments
	- 1. Personalization beats a one-size-fits-all formula — the optimizer fits parameters to the individual's actual review data.
	- 2. It's a clean break from SM-2, not a tuning of it — enabling FSRS makes Ease Factor and New Interval settings irrelevant.
	- 3. It's explicitly scoped — not designed for incremental-reading workflows, and several interval-modifying add-ons are flagged incompatible.
- ## Concepts Introduced
	- [[wiki/concepts/fsrs]] —
- ## Evidence Quality
	- **Moderate for descriptive claims** (what FSRS is, who built it, how it's used) — this is the primary-source README, so those facts are well grounded.
	- **Weak for performance claims** — no benchmark numbers or study results were present in the ingested text; two academic papers are cited by title only. Do not treat "FSRS is better than SM-2" as sourced from this ingest.
- ## My Take
	- *RESERVED FOR HUMAN CURATOR.*
- ## Follow-Up Questions
	- Worth ingesting the two cited papers (KDD, TKDE) directly to get the actual benchmark data and the difficulty/stability/retrievability model details.
	- Worth a `wiki/concepts/spaced-repetition` page as the parent concept — this test ingest only built the FSRS-specific page, since that's what the source actually covered.
