title:: wiki/concepts/activity-taxonomy
type:: concept
created:: 2026-10-21
updated:: 2026-10-21
status:: draft
category:: pedagogy
sources:: vocab-games `docs/learning-design-checks.md`, `docs/claude-reference/exercise-framework.md`, `docs/INVENTORY.md` (internal repo docs, read 2026-10-21; no external literature)
related:: [[mem/projects/ai-activities-website]], [[wiki/concepts/fsrs]], [[wiki/concepts/geo]]
tags:: activities, taxonomy, exercise-types, vocab-games

- ## Definition
	- An activity taxonomy is a fixed vocabulary of activity types, each defined by what the learner does, how the answer is checked, and what feedback follows. The AI-activities generator needs one before it can emit typed, checkable activities instead of free-form text (the blocker named in [[mem/projects/ai-activities-website]]).
	- This is a **working draft inferred from what `vocab-games` (englishonline.training) already ships**. It is not drawn from the learning-science literature, and no paper has been ingested for it yet.
- ## Key Insights
	- Types observed in the live exercise framework, by how they are marked:
		- **Gap-fill (dropdown)** — the dominant type (most common label in `docs/INVENTORY.md`). Auto-scored per gap. Partial credit by attempt number: 1st check = 1, 2nd = ½, 3rd = ¼, later = 0. Wrong answers get a one-line `why` on the results screen.
		- **Multiple choice** — a variant of the above, used occasionally.
		- **Matching / sentence matching** — join halves, terms to definitions, or events in order.
		- **Reading text + comprehension questions** — a text with the target structure bolded on its first 2–3 occurrences, followed by questions.
		- **Dialogue** — appears in the inventory; no scoring detail was checked.
		- **Free writing** — a textarea with a self-check rubric in practise mode. Not auto-scored; the prompt must name a situation, an audience and a purpose.
		- **Recall prompt** — an optional textarea that opens Exercise A. Deliberately unmarked and not in any answer key, because recall helps even when the answer is wrong.
		- **Spaced-review items** — 1–2 gap items per page pulled from an earlier page, plus generated `*-review.html` pages.
	- Suggested axes for the taxonomy (my synthesis, not a sourced model): **response mode** (select / construct / free-produce), **checkability** (auto-scored / self-checked / unmarked), **cognitive move** (recall, recognise, apply, produce) and **target** (vocabulary / grammar / reading / writing).
	- The repo's rules map onto the generator's constraints: one target point per section, instructions stated once, an outcome phrased as an action ("you can …"), and feedback that says *which* items were wrong.
- ## In Practice
	- Unchecked types need a different generation contract. An auto-scored type needs an answer key and an explanation per item. A free-write type needs a scenario and a rubric.
	- The existing `data/explanations.json` shape (`gaps: {id: {label, correct, why, accept?}}`) is already a typed contract for gap-fill and is a candidate schema for generated items.
	- A first template (the "quiz variant" in the project's next actions) should start from gap-fill, the best-specified type here.
- ## Connections
	- [[mem/projects/ai-activities-website]] — the project this page unblocks
	- [[wiki/concepts/fsrs]] — scheduling for the spaced-review types
	- [[wiki/concepts/geo]] — shares the "typed, self-contained chunks" idea, applied to site content rather than activities
- ## Contradictions
	- None found. There is a single source (the repo), and it is the user's own.
- ## Open Questions
	- Which learning-science taxonomy should anchor the axes (retrieval practice, Bloom-style levels, something else)? Needs sourced literature, not extrapolation from the repo.
	- The type list reflects only what the repo ships. Types the generator could add (cloze from a text, error correction, reordering) are not covered.
	- Counts and labels come from `docs/INVENTORY.md` and may lag the live site. The exercise code was not audited for other types.
