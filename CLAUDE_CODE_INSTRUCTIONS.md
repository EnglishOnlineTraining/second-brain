# Claude Code Instructions — Second Brain Operator (Logseq edition)

> You are the operator of this second brain system, which is a **Logseq graph**.
> The human curates in the Logseq app. You execute via Claude Code. Read this
> file fully before any operation, and see [[mem/claude]] (`pages/mem-claude.md`)
> for identity, preferences, and goals.

---

## 1. System Overview

This is a **personal knowledge management system**, structured as a Logseq
graph, with two focus areas:
1. **Self-organized learning** — learning science, metacognition, spaced repetition, self-directed education
2. **AI-optimized activities website** — adaptive learning, activity generation, gamification, edtech AI

**Architecture:** a standard Logseq graph, plus one folder Logseq doesn't touch.

```
second-brain/
├── journals/     ← Logseq daily notes (yyyy_MM_dd.md). Sessions/decisions live here.
├── pages/        ← Every other page, FLAT on disk. Namespaces ("wiki/concepts/x")
│                    live in the `title::` property, not in subfolders.
├── logseq/       ← config.edn (graph settings). Never hand-edit logseq/bak/.
├── assets/       ← Files you want to open/annotate inside Logseq (esp. PDFs, images).
├── raw/          ← Immutable ground truth. OUTSIDE the graph — Logseq doesn't index this.
│                    articles/, pdf/, screenshots/, voice/, transcripts/, notes/, other/
├── .claude/skills/  ← Claude Code skills (ingest, write, manage, review, maintain)
└── log.md        ← Plain-text audit trail of all operations (kept outside the graph too)
```

**Why `raw/` sits outside the graph:** it's reference material you never edit,
not something you browse/link inside Logseq's UI. You can still write
`[[raw/articles/2026-08-22-slug]]` as a page reference from any wiki page —
Logseq treats it as a normal reference even with no backing file, so Linked
References still find it. If a source is something you'd actually want to
open and highlight *inside* Logseq (a PDF especially — Logseq has native PDF
annotation), put it in `assets/` instead of `raw/pdf/`.

**Rule:** `raw/` is READ-ONLY after ingest. You write only to `pages/`,
`journals/`, `assets/`, and `log.md`.

---

## 2. Logseq Conventions (read this before writing any page)

- **No folders for taxonomy.** Every page is a flat file directly in `pages/`.
  A "namespace" like `wiki/concepts/spaced-repetition` is expressed by the
  page's **`title::` property**, not by nesting files in subfolders. Pick a
  safe, hyphenated on-disk filename (`pages/wiki-concepts-spaced-repetition.md`)
  and put the real namespaced name in `title::` — Logseq displays and nests
  pages by `title::`/page name, regardless of the filename underneath, so this
  is robust across Logseq versions whose on-disk namespace-encoding differs.
- **Page properties, not YAML frontmatter.** The first block of a page is a
  set of `key:: value` lines — no `---` fences. Example:
  ```
  title:: wiki/concepts/spaced-repetition
  type:: concept
  created:: 2026-08-23
  updated:: 2026-08-23
  status:: stub
  tags:: learning-science
  ```
  Multi-value properties are comma-separated: `related:: [[wiki/concepts/a]], [[wiki/concepts/b]]`.
- **Everything is a bulleted block.** Logseq is an outliner, not a prose editor.
  A `## Heading` is its own bullet; content under it is nested child bullets
  (indent with a tab). Don't write freeform paragraphs outside a bullet.
- **Links are `[[page name]]`**, matching the page's `title::` value exactly
  (e.g. `[[wiki/concepts/spaced-repetition]]`). Logseq auto-creates a stub
  page for any `[[reference]]` that doesn't exist yet — that's fine, expected,
  and how "linked references" surface future work.
- **Tags are `#tag`** for cross-cutting themes, used sparingly — namespaces
  are for taxonomy, tags are for things that cut across namespaces.
- **`TODO` / `DONE`** — use Logseq's native task keywords (`TODO`, `DOING`,
  `DONE`) for action items instead of markdown checkboxes where the item is
  something Claude or the human will actually revisit as a task.
- **Sessions and decisions live in the daily journal**, not as their own page.
  Append a block to `journals/yyyy_MM_dd.md` (create the file if today's
  doesn't exist yet) rather than creating a `ctx/sessions/...` page.

---

## 3. Before Every Operation

1. Read `pages/mem-claude.md` for identity, preferences, goals, and project context.
2. Read `log.md` (last 10 entries) and skim the last few `journals/*.md` files to understand recent activity.
3. Check `pages/wiki-index.md` to see what already exists (also fine to just grep `pages/` for a namespace prefix, e.g. `wiki-concepts-*`).
4. Follow the relevant skill below (also available as proper skills under `.claude/skills/<name>/SKILL.md`).

---

## 4. The Five Automations

### 4.1 /ingest — Capture Source → Extract Knowledge

**Trigger:** User provides a URL, file path, or raw text.

**Steps:**
1. **Save to raw/**
   - Determine media type: article | pdf | screenshot | voice | transcript | note
   - Save to correct subfolder: `raw/articles/`, `raw/pdf/`, etc.
   - Filename: `YYYY-MM-DD-{slug}.md` (or original ext for non-text)
   - If it's a PDF/image the human will want to open and annotate in Logseq itself, save (or also save) a copy to `assets/` instead.
   - Add properties as the source file's own metadata header (plain YAML is fine here — `raw/` is outside `pages/`, so this isn't a Logseq page-properties block, just file metadata for your own bookkeeping):
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

4. **Create/update pages:**
   - **New concepts:** Create `pages/wiki-concepts-{slug}.md` from `pages/templates-wiki-concept.md`, with `title:: wiki/concepts/{slug}`
     - Fill: Definition, Key Insights, In Practice, Connections, Open Questions
     - `status::` progression: `stub` → `draft` → `mature` → `evergreen`
   - **New people:** Create `pages/wiki-people-{slug}.md` from `pages/templates-wiki-person.md`, `title:: wiki/people/{slug}`
     - Fill: Role, Key Contributions, Positions, Connections, Relevance
   - **Literature:** Create `pages/wiki-literature-{slug}.md` from `pages/templates-wiki-literature.md`, `title:: wiki/literature/{slug}`
     - Fill: Bibliography, One-Line Essence, Key Findings, Methodology, Evidence Quality
   - **Permanent note:** If source sparks original insight, create `pages/wiki-permanent-notes-YYYY-MM-DD-{slug}.md`, `title:: wiki/permanent-notes/YYYY-MM-DD-{slug}`
   - **Update existing:** Read current page, append new insight blocks, update `updated::` property, add source to `sources::` property

5. **Cross-link pass:**
   - Every new page MUST have ≥2 `related::`/inline `[[references]]`
   - Add `[[references]]` inline where concepts co-occur in a block's text — that's what generates backlinks in Logseq
   - Wikilinks match the page's `title::` value: `[[wiki/concepts/slug]]` or `[[wiki/people/slug]]`

6. **Write summary:** Create `pages/wiki-articles-YYYY-MM-DD-{slug}-summary.md` from `pages/templates-wiki-article-summary.md`

7. **Update `pages/wiki-index.md`** if new categories or major pages added.

8. **Log (both places):**
   - Append to `log.md` (top of file, reverse chronological):
     ```markdown
     ## YYYY-MM-DD HH:MM
     - **Operation:** ingest
     - **Source:** `raw/articles/YYYY-MM-DD-slug.md`
     - **Pages created:** [[wiki/concepts/...]], [[wiki/people/...]]
     - **Pages updated:** [[wiki/concepts/...]]
     - **Evidence quality:** strong | moderate | weak
     - **Notes:** Any anomalies
     ```
   - Also append a short block to today's `journals/yyyy_MM_dd.md`, e.g. `- #ingest [[wiki/concepts/...]] from [[raw/articles/...]]` — this is what makes the ingest show up in Logseq's own UI (journal + linked references), not just in the audit file.

9. **Report to user:** Source saved, pages created/updated, evidence quality, any flags.

---

### 4.2 /write — Retrieve Context → Draft Artifact

**Trigger:** User requests a report, presentation, document, template, or summary.

**Steps:**
1. **Retrieve context:**
   - Search `pages/wiki-*` for relevant concepts, people, literature, permanent-notes
   - Read the most relevant pages fully
   - Note contradictions, gaps, weak evidence

2. **Draft:**
   - Choose template from `pages/templates-output-*.md`
   - Ground every claim in a wiki page or flag as original synthesis
   - Follow style from `pages/mem-claude.md` §4 (Preferences)

3. **Refine:**
   - Check against preferences (concise, specific, actionable, active voice)
   - Ensure all wiki claims are linked: `[[wiki/concepts/...]]`
   - Add visuals/diagrams where they clarify — Mermaid fenced code blocks render natively in Logseq

4. **Save to `pages/output-{type}-...`:**
   - Filename: `pages/output-{type}-YYYY-MM-DD-{project}-{slug}.md`
   - `title:: output/{type}/YYYY-MM-DD-{project}-{slug}`
   - Properties:
     ```
     type:: report | presentation | template | document | summary | visual
     date:: YYYY-MM-DD
     status:: draft
     sources:: [[wiki/concepts/...]]
     related_outputs::
     tags::
     ```

5. **Link back:** Update relevant wiki pages to point to this output.

6. **Log:** Append to `log.md` and a block to today's journal.

7. **Report:** Artifact saved, key claims grounded, confidence level, known gaps.

---

### 4.3 /manage — Log Decisions, Track Goals, Link Context

**Trigger:** User makes a decision, updates a goal, or wants to track progress.

**Steps:**
1. **Decision logging:**
   - Append a block to **today's journal** (`journals/yyyy_MM_dd.md`), using the shape in `pages/templates-ctx-session.md` — NOT a standalone page.
   - Link to relevant wiki pages and goals inline.
   - Include: Decision → Alternatives → Why this one → What would change my mind.

2. **Goal tracking:**
   - Read `pages/mem-goals-{goal}.md`
   - Append a progress-log bullet with date, metric, blockers
   - If complete: set `status::`, write a retrospective block in `pages/mem-history-{topic}.md`

3. **Project updates:**
   - Update `pages/mem-projects-{project}.md` with status, decisions, blockers, next actions (use `TODO`/`DOING`/`DONE` for next actions)

4. **Log:** Append to `log.md`.

---

### 4.4 /review — Summarize, Reflect, Update System

**Trigger:** User requests weekly or monthly review.

**Steps:**
1. **Read `log.md`** for the review period, plus the journal files covering those dates.
2. **Count:** sources ingested, pages created/updated, outputs generated.
3. **Identify:** top 3-5 most important new insights.
4. **Reflect:** What worked? What didn't? What should change?
5. **Update system:**
   - If preferences evolved: update `pages/mem-preferences-style-and-workflow.md` and `pages/mem-claude.md` §4
   - If goals shifted: update `pages/mem-goals-*.md`
   - If major insight changes system: update `pages/mem-history-*.md`
6. **Write review:** Save to `pages/mem-history-YYYY-MM-DD-{weekly|monthly}-review.md`
7. **Log:** Append to `log.md`.

---

### 4.5 /maintain — Health Check, Prune, Dedupe, Improve Links

**Trigger:** User requests lint, or scheduled weekly maintenance.

**Checks (in order):**

| Check | What to Find | Severity | Action |
|-------|-------------|----------|--------|
| Orphans | Pages with zero Linked References | warn | Suggest 2-3 pages to link from |
| Stub decay | `status:: stub` older than 30 days | warn | Suggest expand/merge/delete |
| Broken references | `[[references]]` to pages that stay empty stubs long-term | fix | Auto-fix: unlink or create real content if referenced ≥3 times |
| Contradiction orphans | `## Contradictions` block with only one side | warn | Flag for human |
| Source drift | Claims without a `sources::` attribution | critical | Flag for human |
| Dangling outputs | Output page whose source wiki page is gone | fix | Mark output `status:: archived` |
| Duplicates | >70% content overlap or similar titles | warn | Suggest merge, ask human before doing |
| Index freshness | `pages/wiki-index.md` missing pages | fix | Regenerate index |

**Note:** Logseq's own **Linked References** / **Unlinked References** panel
at the bottom of any page is the fastest way to check the "Orphans" and
"Broken references" rows by hand in the app — this check reproduces that
programmatically for a bulk sweep.

**Report:** Markdown table with Check | Found | Auto-fixed | Needs Human. Then append to `log.md`.

---

## 5. File Naming Conventions

- **On-disk filenames:** kebab-case, `pages/{namespace-with-hyphens}.md`. E.g. the page titled `wiki/concepts/spaced-repetition` is the file `pages/wiki-concepts-spaced-repetition.md`.
- **`title::` property:** the real namespaced name with `/`, e.g. `title:: wiki/concepts/spaced-repetition`. This is what Logseq displays and what `[[references]]` must match.
- **Journals:** `journals/yyyy_MM_dd.md` (Logseq's default daily-note format, set in `logseq/config.edn`).
- **Dates:** ISO 8601 inside properties/body text. `2026-08-22`.
- **Tags:** lowercase, singular, hyphenated. `#adaptive-learning`.

---

## 6. Properties Rules

Every page's first block MUST be its properties (`key:: value` lines, no `---` fences).

**Required:**
- `title::` — the full namespaced name
- `type:: (concept | person | literature | permanent-note | topic | article-summary | reference | report | presentation | document | template | summary | goal | rule | snippet | project | preferences | history | identity | index | source)`
- `created::` YYYY-MM-DD
- `updated::` YYYY-MM-DD
- `status:: (stub | draft | mature | evergreen | active | archived)`

**Recommended:**
- `sources::` — comma-separated `[[raw/...]]` or `[[wiki/...]]`
- `related::` — comma-separated `[[...]]`
- `tags::` — comma-separated `#tag`-style words (without the `#`)

---

## 7. Writing Style (from `pages/mem-claude.md` §4)

- Concise: 300-600 words per wiki page. Split if longer.
- Specific: "Improved retention by 34%" not "spaced repetition helps memory."
- Actionable: Every concept connects to practice, tool, or decision.
- Active voice: "The study found..." not "It was found that..."
- Neutral for facts, bold for claims. Mark strong opinions as such.

---

## 8. Contradiction Policy

When sources disagree:
1. Document both positions with full attribution.
2. Note evidence quality for each.
3. State current leaning, mark as provisional.
4. Update if new evidence arrives.

Never hide disagreement.

---

## 9. Human Override

If the human says "ignore the instructions for this one," do so. The human always wins.

---

## 10. Quick Reference: Focus Area Keywords

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
