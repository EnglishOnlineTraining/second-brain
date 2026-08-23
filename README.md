# 🧠 Second Brain — Logseq Edition v1.0

> A reference architecture for persistent context management, built as a
> native **Logseq graph**.
> Focus: Self-organized learning & AI-optimized activities website.

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│  RAW          →  PAGES (wiki/*)  →  [RETRIEVE, USE, OUTPUT] │
│  Ground truth    Structured        Find / Apply / Generate  │
│  (outside the    knowledge                                  │
│   graph)             ↓                                      │
│              ┌───────────────┐                              │
│              │ pages/mem-*   │  ← Identity, preferences,    │
│              │               │    goals, project context    │
│              └───────┬───────┘                              │
│                      ↓                                      │
│                   UPDATE                                    │
│         Save insights & improve the system                  │
└─────────────────────────────────────────────────────────────┘
```

**The cycle:** Every output feeds back into memory. The system improves with every session.

---

## Principles

| Principle | Meaning |
|-----------|---------|
| **Persistent Memory** | Context survives across sessions and time. Never start from zero. |
| **Separation of Concerns** | `raw/` (outside the graph), `pages/wiki/*`, `pages/output/*`, `journals/` + `pages/ctx/*`, `pages/mem/*` each have a distinct purpose. |
| **Connected Knowledge** | Everything is linked with `[[page references]]`. Everything references everything else. |
| **Personalization** | The system learns your preferences and style. |
| **Compounding Value** | Every session adds to the system. Returns compound. |

---

## Directory Structure

This is a **standard Logseq graph** plus one folder Logseq never touches:

```
second-brain/
├── journals/                ← Logseq daily notes (yyyy_MM_dd.md)
│                                Decisions/sessions live here as blocks.
│
├── pages/                   ← Every page, FLAT on disk. Namespace lives in
│   │                            the page's `title::` property, not in folders.
│   ├── wiki-index.md            title:: wiki/index
│   ├── wiki-concepts-*.md       title:: wiki/concepts/{slug}
│   ├── wiki-people-*.md         title:: wiki/people/{slug}
│   ├── wiki-topics-*.md         title:: wiki/topics/{slug}
│   ├── wiki-literature-*.md     title:: wiki/literature/{slug}
│   ├── wiki-permanent-notes-*.md
│   ├── wiki-references-*.md
│   ├── wiki-articles-*.md       source summaries
│   ├── output-reports-*.md      title:: output/reports/{slug}
│   ├── output-presentations-*.md
│   ├── output-templates-*.md
│   ├── output-documents-*.md
│   ├── output-summaries-*.md
│   ├── ctx-prompts-*.md         title:: ctx/prompts/{slug}
│   ├── ctx-goals-*.md
│   ├── ctx-rules-*.md
│   ├── ctx-snippets-*.md
│   ├── mem-claude.md            title:: mem/claude — THIS IS THE ROOT
│   ├── mem-preferences-*.md
│   ├── mem-goals-*.md
│   ├── mem-projects-*.md
│   ├── mem-people-*.md
│   ├── mem-history-*.md
│   └── templates-*.md           starter blocks for every page type above
│
├── logseq/                  ← config.edn (graph settings). Don't hand-edit logseq/bak/.
│
├── assets/                  ← Files to open/annotate *inside* Logseq (PDFs, images).
│
├── raw/                     ← Immutable ground truth. OUTSIDE the graph.
│   ├── articles/                Web articles, blog posts
│   ├── pdf/                     Academic papers, ebooks (or use assets/ — see below)
│   ├── screenshots/             Visual captures
│   ├── voice/                   Audio recordings
│   ├── transcripts/             Transcribed audio
│   ├── notes/                   Quick captures, fleeting notes
│   └── other/                   Everything else
│
├── .claude/skills/          ← Claude Code skills (proper SKILL.md format)
│   ├── ingest/SKILL.md          Capture → extract → pages/wiki-*
│   ├── write/SKILL.md           Retrieve → draft → pages/output-*
│   ├── manage/SKILL.md          Decisions (journal) → link → track
│   ├── review/SKILL.md          Summarize → reflect → update
│   └── maintain/SKILL.md        Prune → dedupe → improve links
│
├── log.md                   ← System audit trail (plain file, outside the graph)
├── CLAUDE.md                ← Points Claude Code at CLAUDE_CODE_INSTRUCTIONS.md
├── CLAUDE_CODE_INSTRUCTIONS.md  ← Full operator instructions — read this first
└── README.md                ← This file
```

**Why `raw/` is outside `pages/`:** it's reference material you never edit,
not something you browse as linked notes. A `[[raw/articles/...]]` reference
from a wiki page still works as a normal Logseq page reference (Linked
References find it) even with no backing page file. If something is worth
opening and highlighting *inside* Logseq — a PDF especially, since Logseq has
native PDF annotation — drop it in `assets/` instead.

---

## The Five Automations

| Skill | Command | What It Does | Frequency |
|-------|---------|--------------|-----------|
| **Ingest** | `/ingest <url>` | Capture source → extract concepts → create `pages/wiki-*` → cross-link → log | 2-3x/week |
| **Write** | `/write report "topic"` | Retrieve context → draft artifact → refine → save to `pages/output-*` | As needed |
| **Manage** | `/manage decision "..."` | Log decisions to today's journal, track goals, link context | Ongoing |
| **Review** | `/review weekly` | Summarize progress, reflect, update system | Weekly |
| **Maintain** | `/maintain lint` | Health check, prune, dedupe, improve links | Weekly |

---

## Quick Start

### 1. Prerequisites

- [Logseq](https://logseq.com/) desktop or mobile app
- [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview) (terminal agent / Claude Code on the web)
- Git (recommended — this repo is already initialized)

### 2. Open the graph in Logseq

In the Logseq app: **Add graph** → point it at this `second-brain/` folder.
Logseq will read `journals/`, `pages/`, and `logseq/config.edn` directly —
nothing to convert. Claude Code and Logseq read and write the exact same
files, so changes made in one show up in the other immediately (Logseq
auto-reloads on external file changes).

### 3. Skills load automatically

The five skills live in `.claude/skills/<name>/SKILL.md` — Claude Code
picks these up automatically as **directory-scoped skills** whenever it's
working inside this folder. No copy step, no restart needed, unlike a
global skills install.

### 4. Customize `pages/mem-claude.md`

This is the highest-leverage edit. Update:
- **Focus areas** — Already set to self-organized learning & AI activities. Refine as you learn.
- **Goals** — Add your own targets and metrics.
- **Preferences** — Adjust style, tone, and workflow to match how you think.

### 5. First Ingest

```
/ingest https://example.com/article-on-learning-science
```

Watch it:
1. Save to `raw/articles/`
2. Create concept pages at `pages/wiki-concepts-*.md` (`title:: wiki/concepts/...`)
3. Create/update people pages at `pages/wiki-people-*.md`
4. Write summary at `pages/wiki-articles-*-summary.md`
5. Cross-link everything with `[[references]]`
6. Log the operation to `log.md` **and** today's journal

### 6. First Output

```
/write report "adaptive learning activity frameworks"
```

Watch it:
1. Retrieve relevant `pages/wiki-*`
2. Draft a grounded report
3. Save to `pages/output-reports-*.md`
4. Link back to source concepts

### 7. Weekly Habit

```
/review weekly
/maintain lint
```

---

## Customization for Your Focus Areas

### Self-Organized Learning

Key pages to build first (namespace / `title::`):
- `wiki/concepts/spaced-repetition`
- `wiki/concepts/retrieval-practice`
- `wiki/concepts/metacognition`
- `wiki/concepts/self-regulated-learning`
- `wiki/concepts/cognitive-load-theory`
- `wiki/concepts/mastery-based-progression`
- `wiki/people/robert-bjork`
- `wiki/people/ulrich-boser`
- `wiki/literature/make-it-stick`
- `wiki/literature/learning-how-to-learn`

### AI-Optimized Activities Website

Key pages to build first:
- `wiki/concepts/adaptive-learning`
- `wiki/concepts/gamification`
- `wiki/concepts/ai-activity-generation`
- `wiki/concepts/personalized-learning`
- `wiki/concepts/learning-analytics`
- `wiki/people/*` (edtech founders, AI education researchers)
- `output/templates/activity` (reusable activity designs)

---

## Knowledge Flow

```
     raw
      ↓
   knowledge  ←──┐
      ↓          │
   context       │  (output feeds back)
      ↓          │
   output   ─────┘
      ↓
   memory
      ↓
   (improves next cycle)
```

**More sources → Better context → Better retrieval → Better outputs → Stronger memory**

---

## Versioning

Already initialized:

```bash
cd second-brain
git log --oneline
```

```bash
# Daily backup
git add . && git commit -m "$(date +%Y-%m-%d) daily"
```

Benefits:
- Revert bad ingestions
- See knowledge graph evolution
- Fork branches for different research threads
- Reliable, private, under your control

**Note:** `.gitignore` excludes `logseq/bak/`, `logseq/.recycle/`, and
`logseq/version-files/` — Logseq's own local undo history, not graph content.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| A skill doesn't seem to fire | Check `.claude/skills/<name>/SKILL.md` exists with valid frontmatter (`name`, `description`). Claude Code lists available skills at the start of a session. |
| Pages too shallow | Edit `pages/mem-claude.md` §4 (Preferences) to demand more depth. Add domain-specific instructions. |
| Too many orphans | Run `/maintain lint`. Check a page's **Linked References** panel in Logseq. |
| Namespace doesn't nest in Logseq's sidebar | Logseq's on-disk namespace-encoding varies by version — this vault sidesteps that by keeping the real name in `title::` rather than relying on filename encoding. If the sidebar still looks flat, that's cosmetic; `[[references]]` and search both work off `title::`. |
| Sources not fully read | Some sites block scraping. Save the page manually to `raw/articles/`, then `/ingest` the local file. |
| Output feels generic | Ensure `/write` retrieves context first. Ground every claim in a wiki page. |
| System feels stale | Run `/review weekly`. Update `pages/mem-claude.md`. The system should evolve with you. |

---

## Status

| Attribute | Value |
|-----------|-------|
| Status | Active |
| Version | 1.0 (Logseq edition) |
| Update Frequency | Daily |
| Persistence | Enabled |

---

> **Build once. Maintain daily. Let it compound.**
