title:: wiki/concepts/graft
type:: concept
created:: 2026-08-23
updated:: 2026-08-23
status:: stub
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
- ## Connections
	- [[mem/projects/ai-activities-website]] — the caching/incremental-rebuild pattern is a candidate reference for the activity-generation-at-scale question
	- [[wiki/concepts/context-management]] — broader concept this is one instance of (page not yet created)
- ## Contradictions
	- None found yet — only one source (the project's own README) ingested. All benchmark figures below are self-reported by the source, not independently verified.
- ## Open Questions
	- The headline benchmark numbers (SWE-bench correctness 54%→66%, token/cost/time savings) come entirely from the vendor's own README — no independent replication was in the ingested text. Treat as a vendor claim, not established evidence, until a third-party source is found.
	- Is this genuinely relevant enough to this vault's focus areas to keep expanding, or was this a one-off tangential ingest? Worth revisiting at the next `/review`.
