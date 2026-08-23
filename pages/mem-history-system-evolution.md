title:: mem/history/system-evolution
type:: history
tags:: system
created:: 2026-08-22

- ## 2026-08-22: Initialization
	- **Decision:** Adopt the 5-namespace architecture (`raw`, `wiki`, `output`, `ctx`, `mem`) based on the reference architecture diagram.
	- **Reason:** Separation of concerns enables compounding value. Raw is immutable, wiki is structured, output is generated, ctx is interaction primitives, mem is identity.
	- **Impact:** All future operations follow this structure.
- ## 2026-08-23: Migrated to a Logseq graph
	- **Decision:** Rebuilt the vault as a proper Logseq graph (`journals/`, `pages/`, `logseq/config.edn`, `assets/`) instead of an Obsidian-style nested-folder vault.
	- **Reason:** The human's actual PKM app is Logseq, not Obsidian. Logseq requires flat `pages/` files (namespaces expressed via a `title::` property, not folder nesting), block/outline content instead of prose under headings, `key:: value` page-properties instead of YAML frontmatter, and native daily journals instead of one-file-per-decision.
	- **Impact:** `wiki/`, `mem/`, `ctx/`, `output/`, and `templates/` folders were removed; their content moved into `pages/` under namespaced titles (`wiki/concepts/...`, `mem/claude`, etc.). `ctx/sessions/` decision logs now live as blocks in the daily journal instead of one file per session. `raw/` stays outside the graph, unchanged, as reference-only ground truth. The five skills (`ingest`, `write`, `manage`, `review`, `maintain`) were rewritten to the new paths and moved into proper `SKILL.md` folders so Claude Code actually discovers them as skills.
