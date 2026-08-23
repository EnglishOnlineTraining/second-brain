# 🧠 Second Brain Architecture v1.0

> A reference architecture for persistent context management.  
> Focus: Self-organized learning & AI-optimized activities website.

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│  RAW          →  WIKI          →  [RETRIEVE, USE, OUTPUT]   │
│  Ground truth    Structured      Find / Apply / Generate    │
│                  knowledge                                    │
│                      ↓                                      │
│              ┌───────────────┐                              │
│              │   CLAUDE.md   │  ← Identity, preferences,    │
│              │   (mem/)      │    goals, project context    │
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
| **Separation of Concerns** | `raw/`, `wiki/`, `output/`, `ctx/`, `mem/` each have a distinct purpose. |
| **Connected Knowledge** | Everything is linked. Everything references everything else. |
| **Personalization** | The system learns your preferences and style. |
| **Compounding Value** | Every session adds to the system. Returns compound. |

---

## Directory Structure

```
second-brain/
├── raw/                    ← Immutable ground truth
│   ├── articles/           │   Web articles, blog posts
│   ├── pdf/                │   Academic papers, ebooks
│   ├── screenshots/        │   Visual captures
│   ├── voice/              │   Audio recordings
│   ├── transcripts/        │   Transcribed audio
│   ├── notes/              │   Quick captures, fleeting notes
│   └── other/              │   Everything else
│
├── wiki/                   ← Structured, linked knowledge
│   ├── index.md            │   Master index
│   ├── articles/           │   Source summaries
│   ├── concepts/           │   Ideas, frameworks, models
│   ├── people/             │   Individuals of relevance
│   ├── topics/             │   Thematic overviews
│   ├── literature/         │   Books, papers, reviews
│   ├── permanent-notes/    │   Original insights (Zettelkasten)
│   ├── references/         │   Quick-reference entries
│   └── other/              │   Everything else
│
├── output/                 ← Generated artifacts
│   ├── reports/            │   Deep analyses, frameworks
│   ├── presentations/      │   Slide decks, story outlines
│   ├── templates/          │   Reusable designs
│   ├── documents/          │   Formal writing
│   ├── summaries/          │   Condensed syntheses
│   ├── visuals/            │   Diagrams, concept maps
│   └── other/              │   Everything else
│
├── ctx/                    ← Interaction primitives
│   ├── sessions/           │   Conversation logs, decisions
│   ├── prompts/            │   Reusable prompt templates
│   ├── goals/              │   Active and archived goals
│   ├── rules/              │   Domain constraints, guardrails
│   └── snippets/           │   Reusable code/text blocks
│
├── mem/                    ← Identity & system memory
│   ├── claude.md           │   System identity (THIS IS THE ROOT)
│   ├── preferences/        │   Evolving style & workflow prefs
│   ├── goals/              │   Goal definitions & progress
│   ├── projects/           │   Project briefs & status
│   ├── people/             │   People you interact with
│   └── history/            │   Major decisions & pivots
│
├── .claude/skills/         ← Claude Code automation skills
│   ├── ingest.md           │   Capture → extract → wiki
│   ├── write.md            │   Retrieve → draft → output
│   ├── manage.md           │   Decisions → link → track
│   ├── review.md           │   Summarize → reflect → update
│   └── maintain.md         │   Prune → dedupe → improve links
│
├── templates/              ← Starter templates
│   ├── wiki/               │   Concept, person, literature, etc.
│   ├── output/             │   Report, presentation, activity, etc.
│   └── ctx/                │   Session, prompt, goal, etc.
│
├── log.md                  ← System audit trail
└── README.md               ← This file
```

---

## The Five Automations

| Skill | Command | What It Does | Frequency |
|-------|---------|--------------|-----------|
| **Ingest** | `/ingest <url>` | Capture source → extract concepts → create wiki pages → cross-link → log | 2-3x/week |
| **Write** | `/write report "topic"` | Retrieve context → draft artifact → refine → save to `output/` | As needed |
| **Manage** | `/manage decision "..."` | Log decisions, track goals, link context | Ongoing |
| **Review** | `/review weekly` | Summarize progress, reflect, update system | Weekly |
| **Maintain** | `/maintain lint` | Health check, prune, dedupe, improve links | Weekly |

---

## Quick Start

### 1. Prerequisites

- [Obsidian](https://obsidian.md/) (recommended) or any markdown editor
- [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview) (terminal agent)
- Git (optional but strongly recommended)

### 2. Install Skills

Copy skill files to your Claude Code skills directory:

```bash
cp .claude/skills/*.md ~/.claude/skills/
# Or your Claude Code skills path
```

Restart Claude Code. Run `/skills` to verify they're loaded.

### 3. Customize `mem/claude.md`

This is the highest-leverage edit. Update:
- **Focus areas** — Already set to self-organized learning & AI activities. Refine as you learn.
- **Goals** — Add your own targets and metrics.
- **Preferences** — Adjust style, tone, and workflow to match how you think.

### 4. First Ingest

```bash
/ingest https://example.com/article-on-learning-science
```

Watch it:
1. Save to `raw/articles/`
2. Create concept pages in `wiki/concepts/`
3. Create/update people pages in `wiki/people/`
4. Write summary in `wiki/articles/`
5. Cross-link everything
6. Log the operation

### 5. First Output

```bash
/write report "adaptive learning activity frameworks"
```

Watch it:
1. Retrieve relevant wiki pages
2. Draft a grounded report
3. Save to `output/reports/`
4. Link back to source concepts

### 6. Weekly Habit

```bash
/review weekly
/maintain lint
```

---

## Customization for Your Focus Areas

### Self-Organized Learning

Key wiki categories to build first:
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

Key wiki categories to build first:
- `wiki/concepts/adaptive-learning`
- `wiki/concepts/gamification`
- `wiki/concepts/ai-activity-generation`
- `wiki/concepts/personalized-learning`
- `wiki/concepts/learning-analytics`
- `wiki/people/` (edtech founders, AI education researchers)
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

## Versioning (Recommended)

```bash
cd ~/second-brain
git init
git add .
git commit -m "init: second brain v1.0"

# Daily backup
git add . && git commit -m "$(date +%Y-%m-%d) daily"
```

Benefits:
- Revert bad ingestions
- See knowledge graph evolution
- Fork branches for different research threads
- Reliable, private, under your control

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| "Skill not found" | Check Claude Code skills directory. Run `/skills` to list loaded skills. |
| Wiki pages too shallow | Edit `mem/claude.md` §4 (Preferences) to demand more depth. Add domain-specific instructions. |
| Too many orphans | Run `/maintain lint`. Add cross-link pass to your `/ingest` workflow. Use Obsidian Graph View. |
| Sources not fully read | Some sites block scraping. Use Obsidian Web Clipper, then `/ingest` the local file. |
| Output feels generic | Ensure `/write` retrieves context first. Ground every claim in a wiki page. |
| System feels stale | Run `/review weekly`. Update `mem/claude.md`. The system should evolve with you. |

---

## Status

| Attribute | Value |
|-----------|-------|
| Status | Active |
| Version | 1.0 |
| Update Frequency | Daily |
| Persistence | Enabled |
| Last Backup | 2026-08-22 |

---

> **Build once. Maintain daily. Let it compound.**
