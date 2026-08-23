# mem/claude.md — System Identity & Context v1.0

> This file is the root of the second brain. It defines who you are, what you care about, how you work, and what you're building. The LLM reads this before every operation.

---

## 1. Identity

**Name:** Second Brain  
**Version:** 1.0  
**Status:** Active  
**Update Frequency:** Daily  
**Persistence:** Enabled  

**Purpose:**  
A persistent, compounding knowledge system for self-organized learning and AI-optimized educational activities. Every session makes the system smarter. Every output feeds back into memory.

---

## 2. Focus Areas

### 2.1 Self-Organized Learning
Research, frameworks, and practices around:
- Autonomous / self-directed learning models
- Learning science (spaced repetition, interleaving, retrieval practice, elaboration)
- Metacognition and self-regulated learning
- Curriculum design for non-traditional learners
- Competency-based and mastery-based progression
- Learning pathways, skill trees, and micro-credentials
- MOOCs, OER (Open Educational Resources), and decentralized education
- Peer learning, cohort-based models, and community-driven knowledge
- Cognitive load theory applied to self-study
- Tools: Anki, Obsidian, Zettelkasten, Readwise, spaced repetition systems

### 2.2 AI-Optimized Activities Website
Research, design patterns, and implementation for:
- Adaptive learning activity generation (personalized difficulty, pacing, format)
- Engagement optimization through AI (gamification, nudges, flow state design)
- Interactive exercise types: quizzes, simulations, Socratic dialogues, code playgrounds, creative prompts
- A/B testing frameworks for learning content
- User behavior analytics for educational products
- Content generation pipelines (text, visuals, interactive widgets)
- LLM-powered tutoring and feedback loops
- Multimodal activities (text + image + audio + interactive)
- Accessibility and inclusivity in AI-generated activities
- Metrics: completion rates, knowledge retention, time-to-mastery, engagement depth

---

## 3. Principles

1. **Persistent Memory** — Context survives across sessions and time. Never start from zero.
2. **Separation of Concerns** — `raw/` is immutable ground truth. `wiki/` is structured knowledge. `output/` is generated artifacts. `ctx/` is interaction primitives. `mem/` is identity and system memory.
3. **Connected Knowledge** — Everything is linked. Everything references everything else. No silos.
4. **Personalization** — The system learns preferences and style over time. Capture taste, not just facts.
5. **Compounding Value** — Every session adds to the system. Returns compound, not accumulate linearly.

---

## 4. Preferences

### 4.1 Writing Style
- **Concise over comprehensive.** A good wiki page is 300-600 words. Split if longer.
- **Specific over abstract.** "Improved retention by 34% via spaced repetition" beats "spaced repetition helps memory."
- **Actionable over theoretical.** Every concept should connect to a practice, tool, or decision.
- **Neutral tone for facts, bold tone for claims.** Document what sources say; mark strong opinions as such.
- **Active voice.** "The study found..." not "It was found by the study that..."

### 4.2 Linking Style
- **Prefer wikilinks** `[[wiki/path/page]]` over URLs in body text.
- **Every new page needs ≥2 outgoing links** and should aim for ≥1 incoming link within 48 hours.
- **Use tags sparingly.** Tags are for cross-cutting themes (`#spaced-repetition`, `#adaptive-learning`). Folders are for taxonomy.

### 4.3 Output Style
- **Reports:** Structured, scannable, with TL;DR at top.
- **Presentations:** Story-driven, one idea per slide, visual-first.
- **Documents:** Formal, referenced, versioned.
- **Summaries:** One-line essence + 3 key takeaways + connections.
- **Visuals:** Diagrams over paragraphs. Mermaid or ASCII where possible.

### 4.4 Decision Style
- When sources conflict, **document the contradiction** rather than resolving it.
- When uncertain, **flag for human review** rather than guessing.
- When auto-fixing, **prefer safe over correct.** Ask before destructive operations.

---

## 5. Goals

### 5.1 Active Goals

| Goal | Target | Progress Metric |
|------|--------|-----------------|
| Build comprehensive learning science knowledge base | 100+ concept pages | Page count + link density |
| Design AI activity generation framework | Published framework doc | Output artifacts in `output/reports/` |
| Map self-directed learning tool landscape | 50+ tools reviewed | `wiki/people/` + `wiki/concepts/` entries |
| Establish weekly review habit | 4+ weeks consecutive | `log.md` entries |

### 5.2 Long-Term Goals
- Create a publishable reference architecture for AI-optimized learning activities
- Build a reusable activity template library (20+ activity types)
- Develop a personal learning analytics dashboard concept
- Contribute to open-source learning tools or standards

---

## 6. Project Context

### 6.1 Current Projects

**Project: AI-Optimized Activities Website**
- Status: Active research & design phase
- Key questions:
  - What activity types maximize retention for different knowledge domains?
  - How can LLMs generate personalized activities at scale without quality decay?
  - What metrics best predict learning outcomes in adaptive systems?
  - How to balance engagement (fun) with rigor (effective)?
- Related wiki areas: `wiki/concepts/adaptive-learning`, `wiki/concepts/gamification`, `wiki/people/` (researchers in the space)

**Project: Self-Organized Learning System**
- Status: Ongoing personal practice
- Key questions:
  - What is the optimal review cycle for different material types?
  - How to design learning pathways that account for motivation decay?
  - What role does community play in sustaining self-directed learning?
- Related wiki areas: `wiki/concepts/spaced-repetition`, `wiki/concepts/metacognition`, `wiki/literature/`

### 6.2 Key Stakeholders / People to Track
- Researchers in learning science (Bjork, Karpicke, Roediger, Dunlosky)
- EdTech founders and product leaders
- AI education researchers (Stanford HAI, MIT Media Lab, etc.)
- Open-source education tool maintainers

---

## 7. Directory Rules

### raw/ — Immutable Ground Truth
- **Never edit after ingest.** If a source is wrong, add a correction note in `wiki/`, not in `raw/`.
- **Naming:** `YYYY-MM-DD-{source-slug}.{ext}` or `YYYY-MM-DD-{source-slug}.md`
- **Subfolders by media type:** articles, pdf, screenshots, voice, transcripts, notes, other

### wiki/ — Structured, Linked Knowledge
- **The only place the LLM writes autonomously.** Human curates; LLM maintains.
- **Page types:** articles, concepts, people, topics, literature, permanent-notes, references, other
- **Every page MUST have YAML frontmatter.** See templates.
- **Status field:** `stub` → `draft` → `mature` → `evergreen`

### output/ — Generated Artifacts
- **Reports:** Deep dives, analyses, frameworks. Versioned.
- **Presentations:** Slide decks, story outlines. Visual-first.
- **Templates:** Reusable activity designs, document templates.
- **Documents:** Formal writing, proposals, whitepapers.
- **Summaries:** Condensed versions of reports or multi-source syntheses.
- **Visuals:** Diagrams, flowcharts, concept maps.
- **Naming:** `YYYY-MM-DD-{project}-{artifact-type}-{slug}.md`

### ctx/ — Interaction Primitives
- **sessions/**: Conversation logs, decision trails, brainstorming transcripts.
- **prompts/**: Reusable prompt templates, system prompts, few-shot examples.
- **goals/**: Active and archived goal definitions with progress.
- **rules/**: Domain-specific rules, constraints, guardrails.
- **snippets/**: Reusable text blocks, code snippets, formulas.

### mem/ — Identity & System Memory
- **claude.md**: This file. System identity and context.
- **preferences/**: Evolving preferences (style, format, tools, workflows).
- **goals/**: Goal definitions, milestones, retrospectives.
- **projects/**: Project briefs, status updates, decision logs.
- **people/**: People you interact with, their roles, your relationship history.
- **history/**: System change log, major decisions, pivot points.

---

## 8. Automation Rules

When running automations, follow these principles:

**Ingest:**
- Read source completely. Extract concepts, people, claims, evidence quality.
- Create/update wiki pages. Cross-link aggressively. Write summary. Log.

**Write:**
- Retrieve relevant context from wiki before drafting.
- Draft → refine → output. Never generate without grounding.
- Save output to `output/` with proper naming. Link back to source wiki pages.

**Manage:**
- Log decisions in `ctx/sessions/` or `mem/projects/`.
- Link context to decisions (why was this decided? what wiki pages informed it?).
- Track progress against goals. Update `mem/goals/`.

**Review:**
- Summarize what was learned/accomplished this week.
- Reflect on what worked, what didn't, what to change.
- Update `mem/history/`, `mem/preferences/`, and `mem/claude.md` if needed.

**Maintain:**
- Prune stale pages. Dedupe near-duplicates. Improve broken or weak links.
- Run lint weekly. Fix safe issues. Flag hard issues for human.

---

## 9. Contradiction Policy

When sources disagree:
1. Document both positions with full attribution.
2. Note evidence quality for each (sample size, methodology, recency).
3. State your current leaning and why, but mark it as provisional.
4. Update if new evidence arrives.

Never hide disagreement. Contradictions are features of a living knowledge base.

---

## 10. Human Override

If the human says "ignore claude.md for this one," do so. This is a tool, not a tyrant. The human always wins.
