---
type: source
date: 2026-08-23
origin: "https://github.com/NanoNets/Graft (README, via raw.githubusercontent.com)"
media: article
tags: [ai, developer-tools, context-management]
status: extracted
---

# Graft — Extracted Knowledge Base Notes

> Extracted via WebFetch on 2026-08-23. Distilled extraction, not verbatim —
> see `origin` for the primary source. License: MIT.

## What This Is & Problem Solved
Graft is an open-source tool that builds a persistent, structured
understanding of large codebases to accelerate AI coding agents. Framed
problem: "Every task, your coding agent starts blind... it is rebuilding a
picture of a codebase it mapped an hour ago and threw away." Humans onboard
to a codebase once; agents currently onboard every session.

## How It Works
Two LLM-powered passes on top of a deterministic base:
1. **Tier 1 (deterministic, $0):** Tree-sitter parses code into a
   per-symbol wiring graph with scope-aware call resolution.
2. **Pass 1 (LLM, cached):** Summarizes each source file.
3. **Pass 2 (LLM, cached):** Groups summaries into curated nodes
   (subsystems, APIs, concepts) with typed links.

Output: a folder of linked markdown files, one node per system/API/concept,
stored locally in a git-ignored `graft/` cache. Refreshes are structural,
hashing files against the previous build (~3ms) and rebuilding only changed
content.

## Key Metrics & Evidence (self-reported by the source — not independently verified)
- **Controlled benchmark (162 runs, two repos):** token savings +42%,
  tool-call reduction +46%, time savings +60%, correctness unchanged at 93%.
- **SWE-bench Verified (50 real GitHub issues, Claude Sonnet 5):**
  correctness 54% → 66% (+12 pts), token savings +23%, cost savings +19%,
  tool-call savings +25%.
- **PocketBase case study** (Go, ~350 files, 15 tasks): cost −21%,
  wall-clock −14%, all 5 real merged PRs reproduced correctly.

## Architecture & Language Support
Three parsing tiers: full-fidelity/scope-aware (TypeScript, JavaScript,
Python, Go, Java), broad/tree-sitter (Rust, C, C++, C#, Ruby, PHP, Kotlin,
Scala, Swift, Elixir, Solidity, OCaml, Zig, Dart, Clojure), and an opt-in
compiler-grade LSP layer (rust-analyzer, clangd, gopls, pyright,
typescript-language-server). 21 languages total.

## Node Content Structure
Each markdown node has: a plain-English Summary (model-written, cached), a
Crux (key lines lifted from source), Sources (content-hash-tracked file
list), typed Links (`depends_on`, `part_of`, `uses`, `implements`,
`produces`), and Notes (user-written, preserved across regenerations).

## Integration
`npm install -g @nanonets/graft && graft init`. Native Claude Code skill
file, Cursor/Copilot/AGENTS.md integrations, an MCP server (six tools), and
a CLI (`build`, `ask`, `skeleton`, `callers`, `grep`, `map`, `blast`,
`viz`). Provider-agnostic (OpenAI, Anthropic, OpenRouter, Fireworks, Groq,
LiteLLM, local servers). Telemetry is anonymous/opt-out and never
transmits code, paths, symbols, or queries.

## Limitations (as stated in source)
- Crux inlining into nodes is "next," not yet shipped.
- LSP-based call edges are best-effort; without a server installed the
  graph is unchanged.
- Uninitialized submodules stay absent until checked out.
- Broad-tier languages lack scope-aware cross-file resolution.

## Positioning
Explicitly distinguished from RAG (no embeddings/similarity search) and
index-based tools (no database/server to keep warm) — "a real graph you can
read," as markdown with typed edges.
