title:: wiki/concepts/graft
type:: concept
created:: 2026-08-23
updated:: 2026-08-23
status:: draft
category:: ai
sources:: [[raw/articles/2026-08-23-graft-readme]]
related:: [[mem/projects/ai-activities-website]], [[wiki/concepts/context-management]]
tags:: ai, developer-tools, context-management

- ## Definition
	- Graft (NanoNets, open-source, MIT) is a tool that builds a persistent, structured representation of a codebase — as a folder of linked markdown "nodes" (one per subsystem/API/concept) — so an AI coding agent doesn't have to re-explore the whole codebase from scratch every session. It combines a deterministic tree-sitter parse (free, per-symbol wiring graph) with two cached LLM passes (per-file summaries, then curated grouped nodes with typed links).
- ## Key Insights
	- The core framing — "humans onboard to a codebase once, agents onboard every session" — is a persistent-memory problem, structurally similar to what this vault itself exists to solve for a human researcher rather than a coding agent.
	- It explicitly rejects RAG (no embeddings/similarity search) and index/database approaches in favor of "a real graph you can read" as plain markdown with typed edges (`depends_on`, `part_of`, `uses`, `implements`, `produces`) — a design choice worth comparing against this vault's own `[[page reference]]` approach.
	- Refresh cost is near-zero (~3ms) because it hashes files against the previous build and only rebuilds changed content — a concrete "cheap incremental update" pattern.
- ## In Practice
	- Not itself a learning-science or edtech tool — this is a developer-tooling source, ingested because its persistent-context/caching pattern is a plausible engineering reference for "How can LLMs generate personalized activities at scale without quality decay?" (an open key question in [[mem/projects/ai-activities-website]]): the same "summarize once, cache, rebuild only what changed" pattern could apply to generating/updating adaptive learning content instead of code understanding.
- ## Hands-On Test (2026-08-23, first-party — not from the vendor source)
	- Installed globally (`npm install -g @nanonets/graft`) and ran the free deterministic tier (`graft build`, `graft skeleton`, `graft callers`, `graft map`) against the `vocab-games` repo — no LLM `--deep` pass attempted, no API key available in this environment.
	- **Worked as advertised, and fast:** installed cleanly, built a 217-node/420-edge wiring graph over 19 files in 1.3 seconds, zero cost.
	- **`graft skeleton exercise.js`** gave an accurate full function-signature map (66 symbols, correct line ranges) at a genuine, self-reported ~92% token saving vs. reading the file — this part of the vendor's efficiency claim held up under an independent (if small, single-file) test.
	- **Real, concrete limitation found, not in the source material:** `vocab-games` keeps almost all of its actual page logic inline in `<script>` tags inside 220+ HTML files (`config/state/page logic` per that repo's own CLAUDE.md), and Graft's tree-sitter tier only parses standalone `.js`/`.ts`/etc. files — it never looked at the HTML at all. Concretely: `graft callers checkDropdowns` reported exactly **one** caller (`test-scoring.js`), when in reality that function is called from roughly 150+ exercise pages — Graft's call graph was accurate for what it could see, but blind to the majority of this codebase's real usage. Anyone using Graft's caller/hotspot output to judge how central a function is, on a codebase like this, would be misled.
	- **Net take:** genuinely useful, cheap, and honest about its scope for a JS/TS-heavy codebase — but a poor fit for `vocab-games` specifically, where the interesting logic lives inside HTML. Not adopted as an ongoing tool there; reverted the incidental `.gitignore`/`graft/` changes it left behind rather than keep them.
	- Untested: the LLM `--deep` tier (per-file summaries, concept grouping) and the headline SWE-bench/benchmark claims — still vendor-only evidence, unresolved from the open question below.
- ## Connections
	- [[mem/projects/ai-activities-website]] — the caching/incremental-rebuild pattern is a candidate reference for the activity-generation-at-scale question
	- [[wiki/concepts/context-management]] — broader concept this is one instance of (page not yet created)
- ## Contradictions
	- None found yet — only one source (the project's own README) ingested. All benchmark figures below are self-reported by the source, not independently verified.
- ## Open Questions
	- The headline benchmark numbers (SWE-bench correctness 54%→66%, token/cost/time savings) still come entirely from the vendor's own README — the hands-on test above checked the free/deterministic tier's *mechanics*, not those specific numbers. Still a vendor claim, not established evidence.
	- Resolved (partially): this was a one-off tangential ingest for `vocab-games` — the hands-on test found it a poor structural fit there (HTML-inline logic it can't see). Whether it'd be worth trying on a JS/TS-heavier codebase later is still open.
