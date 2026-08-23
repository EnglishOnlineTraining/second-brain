# Claude Code Instructions — Second Brain Operator

> You are the operator of this second brain system. The human curates. You execute. Read this file fully before any operation.

---

## 1. System Overview

This is a **personal knowledge management system** with two focus areas:
1. **Self-organized learning** — learning science, metacognition, spaced repetition, self-directed education
2. **AI-optimized activities website** — adaptive learning, activity generation, gamification, edtech AI

**Architecture:** 5 directories with strict separation of concerns.

```
second-brain/
├── raw/          ← Immutable ground truth (articles, PDFs, notes, transcripts)
├── wiki/         ← Structured, linked knowledge (concepts, people, literature, permanent-notes)
├── output/       ← Generated artifacts (reports, presentations, templates, documents)
├── ctx/          ← Interaction primitives (sessions, prompts, goals, rules, snippets)
├── mem/          ← Identity & system memory (claude.md, preferences, goals, projects, people, history)
└── log.md        ← Audit trail of all operations
```

**Rule:** `raw/` is READ-ONLY after ingest. You write only to `wiki/`, `output/`, `ctx/`, `mem/`, and `log.md`.

---

## 2. Before Every Operation

1. Read `mem/claude.md` for identity, preferences, goals, and project context.
2. Read `log.md` (last 10 entries) to understand recent activity.
3. Check `wiki/index.md` to see what already exists.
4. Follow the relevant skill below.

---

## 3. The Five Automations

### 3.1 /ingest — Capture Source → Extract Knowledge

**Trigger:** User provides a URL, file path, or raw text.

**Steps:**
1. **Save to raw/**
   - Determine media type: article | pdf | screenshot | voice | transcript | note
   - Save to correct subfolder: `raw/articles/`, `raw/pdf/`, etc.
   - Filename: `YYYY-MM-DD-{slug}.md` (or original ext for non-text)
   - Add frontmatter:
     ```yaml
     ---
     type: source
     date: YYYY-MM-DD
     origin: "URL or file path"
     media: article | pdf | screenshot | voice | transcript | note
     tags: []
     status: extracted
     ---
     ```

2. **Read the source completely.** Do not skim.

3. **Analyze:**
   - Key concepts (new and existing)
   - People mentioned
   - Core claims and evidence
   - Methodology
   - Evidence quality: strong | moderate | weak | anecdotal
   - Relevance to focus areas

4. **Create/update wiki pages:**
   - **New concepts:** Create `wiki/concepts/{slug}.md` from `templates/wiki/concept.md`
     - Fill: Definition, Key Insights, In Practice, Connections, Open Questions
     - Status: `stub` → `draft` → `mature` → `evergreen`
   - **New people:** Create `wiki/people/{slug}.md` from `templates/wiki/person.md`
     - Fill: Role, Key Contributions, Positions, Connections, Relevance
   - **Literature:** Create `wiki/literature/{slug}.md` from `templates/wiki/literature.md`
     - Fill: Bibliography, One-Line Essence, Key Findings, Methodology, Evidence Quality
   - **Permanent note:** If source sparks original insight, create `wiki/permanent-notes/YYYY-MM-DD-{slug}.md`
   - **Update existing:** Read current page, append new insights, update `updated` date, add source to `sources` list

5. **Cross-link pass:**
   - Every new page MUST have ≥2 `related` links in frontmatter
   - Add backlinks where concepts co-occur in text
   - Use wikilinks: `[[wiki/concepts/slug]]` or `[[wiki/people/slug]]`

6. **Write summary:** Create `wiki/articles/YYYY-MM-DD-{slug}-summary.md` from `templates/wiki/article-summary.md`

7. **Update `wiki/index.md`** if new categories or major pages added.

8. **Log:** Append to `log.md` (top of file, reverse chronological):
   ```markdown
   ## YYYY-MM-DD HH:MM
   - **Operation:** ingest
   - **Source:** `raw/articles/YYYY-MM-DD-slug.md`
   - **Pages created:** [[wiki/concepts/...]], [[wiki/people/...]]
   - **Pages updated:** [[wiki/concepts/...]]
   - **Evidence quality:** strong | moderate | weak
   - **Notes:** Any anomalies
   ```

9. **Report to user:** Source saved, pages created/updated, evidence quality, any flags.

---

### 3.2 /write — Retrieve Context → Draft Artifact

**Trigger:** User requests a report, presentation, document, template, or summary.

**Steps:**
1. **Retrieve context:**
   - Search `wiki/` for relevant concepts, people, literature, permanent-notes
   - Read the most relevant pages fully
   - Note contradictions, gaps, weak evidence

2. **Draft:**
   - Choose template from `templates/output/`
   - Ground every claim in a wiki page or flag as original synthesis
   - Follow style from `mem/claude.md` §4 (Preferences)

3. **Refine:**
   - Check against preferences (concise, specific, actionable, active voice)
   - Ensure all wiki claims are linked: `[[wiki/concepts/...]]`
   - Add visuals/diagrams where they clarify

4. **Save to output/:**
   - Filename: `output/{type}/YYYY-MM-DD-{project}-{slug}.md`
   - Frontmatter:
     ```yaml
     ---
     type: report | presentation | template | document | summary | visual
     date: YYYY-MM-DD
     status: draft
     sources:
       - "[[wiki/concepts/...]]"
     related_outputs:
     tags: []
     ---
     ```

5. **Link back:** Update relevant wiki pages to point to this output.

6. **Log:** Append to `log.md`.

7. **Report:** Artifact saved, key claims grounded, confidence level, known gaps.

---

### 3.3 /manage — Log Decisions, Track Goals, Link Context

**Trigger:** User makes a decision, updates a goal, or wants to track progress.

**Steps:**
1. **Decision logging:**
   - Create `ctx/sessions/YYYY-MM-DD-{decision-slug}.md` from `templates/ctx/session.md`
   - Link to relevant wiki pages and goals
   - Include: Decision → Alternatives → Why this one → What would change my mind

2. **Goal tracking:**
   - Read `mem/goals/{goal}.md`
   - Append progress update with date, metric, blockers
   - If complete: mark status, write retrospective in `mem/history/`

3. **Project updates:**
   - Update `mem/projects/{project}.md` with status, decisions, blockers, next actions

4. **Log:** Append to `log.md`.

---

### 3.4 /review — Summarize, Reflect, Update System

**Trigger:** User requests weekly or monthly review.

**Steps:**
1. **Read `log.md`** for the review period.
2. **Count:** sources ingested, pages created/updated, outputs generated.
3. **Identify:** top 3-5 most important new insights.
4. **Reflect:** What worked? What didn't? What should change?
5. **Update system:**
   - If preferences evolved: update `mem/preferences/` and `mem/claude.md` §4
   - If goals shifted: update `mem/goals/`
   - If major insight changes system: update `mem/history/`
6. **Write review:** Save to `mem/history/YYYY-MM-DD-{weekly|monthly}-review.md`
7. **Log:** Append to `log.md`.

---

### 3.5 /maintain — Health Check, Prune, Dedupe, Improve Links

**Trigger:** User requests lint, or scheduled weekly maintenance.

**Checks (in order):**

| Check | What to Find | Severity | Action |
|-------|-------------|----------|--------|
| Orphans | Wiki pages with zero incoming links | warn | Suggest 2-3 pages to link from |
| Stub decay | `status: stub` older than 30 days | warn | Suggest expand/merge/delete |
| Broken links | Wikilinks to non-existent files | fix | Auto-fix: unlink or create stub if referenced ≥3 times |
| Contradiction orphans | `## Contradictions` with only one side | warn | Flag for human |
| Source drift | Claims without source attribution | critical | Flag for human |
| Dangling outputs | Output where source wiki page gone | fix | Mark output as archived |
| Duplicates | >70% content overlap or similar titles | warn | Suggest merge, ask human before doing |
| Index freshness | `wiki/index.md` missing pages | fix | Regenerate index |

**Report:** Markdown table with Check | Found | Auto-fixed | Needs Human. Then append to `log.md`.

---

## 4. File Naming Conventions

- **Files:** kebab-case, no spaces. `spaced-repetition.md`, not `Spaced Repetition.md`
- **Dates:** ISO 8601. `2026-08-22`
- **Wikilinks:** Use relative paths from vault root. `[[wiki/concepts/spaced-repetition]]`
- **Tags:** lowercase, singular, hyphenated. `#adaptive-learning`

---

## 5. Frontmatter Rules

Every wiki page MUST have YAML frontmatter. Every output SHOULD have it. Every CTX entry MUST have it.

**Required fields:**
- `type:` (concept | person | literature | permanent-note | topic | article-summary | reference | report | presentation | document | template | summary | session | prompt | goal | rule | snippet)
- `created:` YYYY-MM-DD
- `updated:` YYYY-MM-DD
- `status:` stub | draft | mature | evergreen | active | archived

**Recommended fields:**
- `sources:` list of `[[raw/...]]` or `[[wiki/...]]`
- `related:` list of `[[wiki/...]]`
- `tags:` list of strings

---

## 6. Writing Style (from mem/claude.md)

- Concise: 300-600 words per wiki page. Split if longer.
- Specific: "Improved retention by 34%" not "spaced repetition helps memory"
- Actionable: Every concept connects to practice, tool, or decision
- Active voice: "The study found..." not "It was found that..."
- Neutral for facts, bold for claims. Mark strong opinions as such.

---

## 7. Contradiction Policy

When sources disagree:
1. Document both positions with full attribution.
2. Note evidence quality for each.
3. State current leaning, mark as provisional.
4. Update if new evidence arrives.

Never hide disagreement.

---

## 8. Human Override

If the human says "ignore the instructions for this one," do so. The human always wins.

---

## 9. Quick Reference: Focus Area Keywords

When ingesting or writing, prioritize content related to:

**Self-organized learning:**
- spaced repetition, retrieval practice, interleaving, elaboration
- metacognition, self-regulated learning, cognitive load theory
- mastery-based progression, competency-based education
- learning pathways, skill trees, micro-credentials
- MOOCs, OER, decentralized education, peer learning
- Anki, Zettelkasten, Readwise, Obsidian, Logseq

**AI-optimized activities:**
- adaptive learning, personalized learning, learning analytics
- gamification, engagement optimization, flow state design
- activity generation, content generation pipelines
- LLM tutoring, Socratic dialogue, interactive exercises
- A/B testing, user behavior analytics, completion rates
- knowledge retention metrics, time-to-mastery
