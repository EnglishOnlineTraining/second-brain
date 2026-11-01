title:: wiki/concepts/activity-taxonomy
type:: concept
created:: 2026-10-21
updated:: 2026-11-01
status:: draft
category:: pedagogy
sources:: vocab-games `docs/learning-design-checks.md`, `docs/claude-reference/exercise-framework.md`, `docs/INVENTORY.md`, `exercise.js`, `data/exercises.json`, `data/quizzes.json` (internal repo files, read 2026-10-21 and 2026-11-01; no external literature)
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
- ## Draft Taxonomy (v2, 2026-11-01)
	- Three grouping axes, each read off what vocab-games ships. Every activity type gets one value per axis. This is a draft for review, not a decision.
	- **1. Skill** — `data/exercises.json` tags each of its 261 pages with one or more skills: writing (167), grammar (139), reading (114), vocabulary (72), listening (20). Pages usually combine several.
	- **2. Interaction format** — what the learner physically does:
		- *Select from a menu* — dropdown gap-fill (`checkDropdowns`) and multi-answer gap-fill (`checkDropdownsMulti`, where a gap accepts an array of valid answers).
		- *Select one of N* — multiple choice, as in `data/quizzes.json` (question, 3 options, one answer; 4 quizzes by level).
		- *Type a short answer* — typed gaps (a `typed` section flag in `exercise.js`; compared after `normAns` normalisation).
		- *Match / order* — join halves, terms to definitions, events in sequence.
		- *Read, then answer* — a text followed by questions.
		- *Listen, then answer* — `initListening`: browser speech synthesis plays a script, capped at 2 plays by default.
		- *Free-produce* — a textarea (writing task, or the unmarked recall prompt).
	- **3. Scoring**
		- *Auto, attempt-weighted* — gap-fill: 1 / ½ / ¼ / 0 by attempt number (`attemptPoints`), with a `why` shown for wrong answers.
		- *Auto, single attempt* — the standalone quizzes: self-scoring, instant total, no sign-up.
		- *Self-checked* — free writing: a rubric in practise mode only, nothing sent anywhere. Class mode sends the text to the teacher.
		- *Unscored* — the recall prompt: deliberately absent from any answer key.
	- Roughly, scoring follows format: select and type formats score automatically, free-produce formats never do. The unusual cell is gap-fill, which is scored on a *process* (attempts) rather than only on the result.
	- Not in the code at all: reorder-the-sentence, error correction, true/false, cloze generated from a text. These are the first generator candidates, because each has a single machine-checkable answer.
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
- ## Decisions Needed
	- These block the first template (the quiz variant) in [[mem/projects/ai-activities-website]].
	- **1. Anchor the taxonomy to a learning-science model, or ship the vocab-games-derived one?** Anchoring (retrieval practice, Bloom-style levels) is better grounded but waits on the paper ingest. Shipping now lets the quiz template start, and the axes can be renamed later.
	- **2. How does the generator handle attempt-weighted scoring?** Quiz-style items are single attempt (all-or-nothing). Gap-fill gives partial credit for later attempts. The quiz variant could use the simple scheme and leave attempt weighting for later, or inherit gap-fill's 1 / ½ / ¼ rule so scores stay comparable across both.
	- **3. Which type does the quiz template cover first?** Options: multiple choice (the shape already in `quizzes.json`, simplest), or dropdown gap-fill (best specified, with a `why` per item, but more fields to generate). A suggested start is multiple choice with a required `why` per option.
