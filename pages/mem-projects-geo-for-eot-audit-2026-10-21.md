title:: mem/projects/geo-for-eot/audit-2026-10-21
type:: project
status:: done
tags:: geo, seo, ai-search, englishonline-training, audit
created:: 2026-10-21
updated:: 2026-10-21

- ## Scope and method
	- Read-only audit of the **activities host** (`vocab-games` repo, `activities.englishonline.training`) against the checklist in [[wiki/concepts/geo]]. Repo at `35941ee` (2026-10-20). Nothing in `vocab-games` or WordPress was edited.
	- Measured by script over every built `*.html` and `themen/*.html` (320 files, 254 indexable after dropping 65 noindex pages and `_template.html`). Counts below are from that run.
	- Read first: `docs/seo-backlog.md` Tiers 7, 8, 10, 11, 13 (headings and bodies). Tiers 9 and 12 were checked only by keyword search for the gaps below. Items already recorded there are cited, not repeated.
	- **Out of scope:** the WordPress main site (covered by the Tier 8 crawl of 2026-10-03 in that backlog) and Core Web Vitals / Search Console data.
- ## Result per checklist item
	- **1. Title, H1 and meta description aligned: PASS, with two notes.**
		- All 254 pages have a `<title>`, a meta description and exactly one `<h1>`. No duplicate titles or descriptions.
		- Only 6 pages have an H1 that shares under half its words with the title. Four are deliberate (exercise H1 is a story title, e.g. `9g-australia-causatives-progressive.html`: title "Causative Verbs & Passive Progressive – Year 9 Australia", H1 "When Did Your Folks Get Here?"). Hub and `themen/` pairs differ in wording but not topic. Keyword-title decision for exercises is already open as A5 in Tier 8.
		- Evidence: `scripts/build-head.js`, built `<head>` blocks.
	- **2. Snippable summaries (Quick Overview, `themen/` prose): PASS for the box, PARTIAL for `themen/`.**
		- Quick Overview ("Auf einen Blick / At a glance") is a static `div.qo-box` on 250 of 254 pages (`build-head.js:441-630`). It is generated HTML, so non-JS crawlers see it. It holds a lede plus a `<dl>` of facts (level, skills, tasks, cost). Missing on `abitur-activities.html`, `msa-activities.html`, `grammar-activities.html`, `uni-presentation-task.html` (hubs and a logistics screen).
		- The lede is the meta description verbatim, so a long description is also a long lede (see gap 1).
		- `themen/` pages: 207 H2-then-paragraph openings across the 18 topic pages, median 14 words, 14 over 45 words, 6 over 60. The long ones are the first "worum geht es?" intro (e.g. `themen/passiv.html`, 164 words, three sentences of explanation plus examples). Headings already name the topic ("Typische Fehler beim Passiv"), done under Tier 10 items 1-3.
	- **3. Schema.org / FAQPage coverage: PASS, and the project page's premise is out of date.**
		- JSON-LD on every indexable page. `LearningResource` 221, `CollectionPage` 214, `BreadcrumbList` 234, `DefinedTermSet` 193, `WebSite` 236, `Person` + `EducationalOrganization` on all 254, `Course` on 3 hubs.
		- `FAQPage` is on **31 pages** (198 Q&A pairs), not 2: all 18 `themen/` topics, the Abitur/MSA/IELTS/IT/Business hubs and others. Every page with a visible FAQ section also has the markup (0 mismatches). Answers median 34 words, max 73, none over 80.
		- Evidence: `scripts/schema.js` (`faqPage`, `learningResource`, `hubPage`), `scripts/validate-schema.js`.
		- **Do not add `Speakable`**: it was deployed site-wide and removed in `d7e4bf6d` because it was flagged as structured-data misuse and the whole subdomain was deindexed around 2026-08-24. Tier 7 and Tier 8 still list it as done, which is stale (gap 5).
	- **4a. Content hidden in tabs or accordions: PASS.**
		- No `role="tab"` anywhere. `<details>` on 7 pages: 2 IELTS reading pages (`passage-copy`, a copy of the reading passage), `uni-c1/c2-vocab-practice`, `10g-south-africa-vocab-practice`, and two Abitur South Africa pages. `<details>` content is in the DOM, so it is readable. The vocab-practice word lists inside `<details>` are filled by JS (`<tbody id="wordlist">` is empty in the source), so they are invisible to non-JS crawlers; low value, the lists are a study aid.
		- Caveat that applies to the whole site and is by design: exercise steps after `#step-0` are shown by JS, so only step 0 (overview box and related links) is guaranteed visible to non-JS crawlers (`build-head.js:446-455`).
	- **4b. Core info only in a PDF or an image: PASS.**
		- PDF links on 4 pages only (`abitur-englisch-2027`, `abitur-operatoren`, `msa-englisch-2027` x4, `property-management-vocabulary`); each is a landing page with HTML text around the link. PDF landing pages are Tier 8 §C item 4.
		- 0 `<img>` without `alt`, 0 with empty `alt` on indexable pages.
	- **4c. Decorative punctuation: FAIL (low severity), not tracked in the backlog.**
		- Em dash: present in body text on 253 of 254 pages, 5 or more on 192 pages. Mostly the generated "Aufgaben: 3 — A · B" row, hub cards and titles. `VOICE.md` v1.0 has no em-dash rule, so this is a judgment call, not a policy breach.
		- Arrow characters on 92 pages; star symbols on 4 (`9c-melbourne-job-application`, `be-company-culture`, `business-activities`, `california-exercises`).
		- 27 H1s start with an emoji (e.g. `abitur-text-analysis.html`: "📖 Text Analysis"). `VOICE.md:58` says "Emojis: none on the website". No emoji in any title or description.
	- **4d. Unanchored buzzwords: PASS.** Searched "next-gen", "cutting-edge", "innovative", "revolutionary", "game-chang*", "state-of-the-art", "world-class", "seamless", "unlock". The only hits are inside exercise passages ("more creative and innovative", "unlocked bike", "Silicon Valley is cutting-edge"), not marketing copy.
- ## Other GEO items checked (not in the original TODO)
	- **robots.txt: PASS.** `User-agent: *` / `Allow: /`, sitemap index listed. No AI crawler block (lifted, Tier 8 A1).
	- **llms.txt: PASS.** 55 lines: one-paragraph summary, grouped links with one-line descriptions, link to the main-site `llms.txt`. No `llms-full.txt` (not wanted; Tier 12 notes Google says AI features need no special file).
	- **Q&A pairs / lists over prose: PASS.** `themen/` pages use a rules list, an examples table and FAQ blocks; `qo-facts` is a `<dl>`.
- ## Gaps not already in `seo-backlog.md`
	- 1. **16 meta descriptions run over 160 characters** (161 to 188): 9 IELTS pages, `10g-south-africa-vocab-practice`, `10g-proud-to-be-black`, `9g-california-future-meaning`, `lead-story-structures`, `uni-c1-vocab-practice`, `uni-c2-vocab-practice`. They are also the Quick Overview lede, so the on-page summary is longer than the one-to-two sentences the checklist wants. Fix in the generator or per page `<meta>`.
	- 2. **27 emoji-prefixed H1s** contradict `VOICE.md:58`. Decide: strip them (heading text and anchor stay) or amend VOICE.md for the activities host.
	- 3. **`themen/` openers over 45 words** (14 sections, 6 over 60, led by the "worum geht es?" intros): add a one-sentence direct answer first. Overlaps Tier 10 item 4 (sub-query map, "each section opens with a one-sentence direct answer"); that item is drafted for `gerund-infinitiv` and `passiv` only, so this is the measured list for the roll-out.
	- 4. **Em-dash, arrow and star symbols in body copy** (see 4c). Optional; no evidence yet they hurt retrieval, and the source behind the checklist is a vendor blog (see [[wiki/concepts/geo]] Contradictions).
	- 5. **Stale `Speakable` lines in `seo-backlog.md`** (Tier 7 intro lines 17 and Tier 7 item 2): they say Speakable is live, but it was removed in `d7e4bf6d` after the deindexing. The `/about/` WordPress page may still carry a `speakable` node (Tier 7 item 2); worth checking in the WordPress half. Needs Shaun.
	- 6. **Four pages lack the Quick Overview box** (`abitur-activities`, `msa-activities`, `grammar-activities`, `uni-presentation-task`). The first three are hubs with their own FAQ; low value.
- ## Verdict
	- Structure for AI search is in good shape on the activities host: aligned metadata, near-total schema and Quick Overview coverage, FAQPage on 31 pages, no hidden-content or buzzword anti-patterns. The remaining gaps are small copy and style fixes. The biggest open GEO items remain in the backlog: indexing (Tier 9) and AI answer tracking (Tier 10.7, Tier 13).
- ## Related
	- [[mem/projects/geo-for-eot]]
	- [[wiki/concepts/geo]]
