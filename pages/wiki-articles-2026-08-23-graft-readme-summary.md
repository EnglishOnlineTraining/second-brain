title:: wiki/articles/2026-08-23-graft-readme-summary
type:: article-summary
created:: 2026-08-23
updated:: 2026-08-23
status:: draft
source:: [[raw/articles/2026-08-23-graft-readme]]
concepts:: [[wiki/concepts/graft]]
people::
tags:: ai, developer-tools

- ## One-Line Essence
	- Graft gives AI coding agents a persistent, cheaply-refreshable markdown map of a codebase instead of making them re-explore it from zero every session.
- ## Key Arguments
	- 1. Persistent, structured context beats session-ephemeral exploration — the "humans onboard once, agents onboard every time" framing.
	- 2. A readable markdown graph with typed edges is positioned as preferable to RAG/embeddings or a database index for this use case.
	- 3. Content-hash-based incremental rebuilds make refresh essentially free (~3ms), which is what makes "always fresh" practical.
- ## Concepts Introduced
	- [[wiki/concepts/graft]] —
- ## Evidence Quality
	- **Weak-to-moderate.** All benchmark numbers (162-run controlled benchmark, SWE-bench Verified results, PocketBase case study) are self-reported in the project's own README, with no independent replication found in this ingest. The descriptive/architectural claims (what it does, how it's built) are well-grounded as a primary source.
- ## My Take
	- *RESERVED FOR HUMAN CURATOR.*
- ## Follow-Up Questions
	- Is there independent (non-vendor) coverage or benchmarking of Graft worth ingesting to test the reported numbers?
	- Does this belong in this vault at all long-term, or was it a one-off tangential test ingest? Flagged in [[wiki/concepts/graft]] for the next `/review`.
