title:: wiki/concepts/geo
type:: concept
created:: 2026-08-23
updated:: 2026-08-23
status:: draft
category:: other
sources:: [[raw/articles/2026-08-23-ai-search-content-optimization]]
related:: [[wiki/concepts/graft]], [[mem/projects/geo-for-eot]]
tags:: geo, seo, ai-search, content-strategy

- ## Definition
	- GEO (Generative Engine Optimization) — also called AIO — is the practice of structuring web content so AI search assistants (Copilot, ChatGPT search, etc.) can **parse** it into small, evaluable pieces and select/assemble those pieces into an answer, rather than just ranking whole pages in a results list. Traditional SEO fundamentals (crawlability, metadata, internal linking, backlinks) are still the baseline, not a replacement.
- ## Key Insights
	- The unit of competition has shifted from *the page* to *the chunk*: assistants break a page into structured pieces (parsing) and evaluate each piece for authority/relevance before assembling an answer, often stitching pieces from multiple sources together.
	- Concrete, checkable claim cited from the source: AI referrals to top websites rose 357% year-over-year in June 2025, reaching 1.13B visits (TechCrunch/SimilarWeb, cited in the source, not independently re-verified here).
	- Specific mechanisms that make content "chunk-friendly": tight title/H1/description alignment, H2/H3s that mark clear idea boundaries, Q&A pairs assistants can lift verbatim, lists/tables over prose, and JSON-LD schema markup that removes ambiguity about what a piece of content *is* (product, FAQ, review, event, etc.).
	- Named anti-patterns worth remembering as concrete, specific rules rather than vague "write clearly" advice: walls of text, answers hidden in tabs/accordions (may not render for AI), core info only in a PDF or only in an image, decorative punctuation (em-dash overuse, arrows, star ratings as symbols), and unanchored buzzwords ("next-gen," "innovative") without a measurable claim behind them.
- ## In Practice
	- Directly, concretely actionable for `vocab-games`/englishonline.training, which already has real infrastructure this maps onto: JSON-LD (`scripts/schema.js`), the `themen/` topic pages' `practice[]` Q&A-style check-yourself widgets, and the `FAQPage` schema already live on `msa-activities.html`/`abitur-mediation.html` (see that repo's CLAUDE.md §5g). This source's checklist is a ready-made audit list for that existing work: are titles/H1s/descriptions tightly aligned site-wide? Are the Quick Overview boxes and topic-page prose snippable (self-contained, 1–2 sentence answers) rather than long paragraphs? Worth a dedicated pass if/when Shaun wants to check `vocab-games` against this.
	- Also a loose structural echo of [[wiki/concepts/graft]]: both are about making content legible to an AI consumer by chunking it into typed, self-contained, machine-parseable pieces rather than one long undifferentiated blob — one for AI search assistants reading a website, the other for AI coding agents reading a codebase.
- ## Connections
	- [[wiki/concepts/graft]] — both concern structuring content into machine-parseable chunks, for different AI consumers
	- [[mem/projects/ai-activities-website]] — content-generation-pipeline question could borrow "snippable, self-contained, typed chunk" thinking from GEO, not just from a code-parsing angle
	- [[mem/projects/geo-for-eot]] — the project this concept now feeds: auditing englishonline.training against this checklist
- ## Contradictions
	- None found yet — single source. Note the source is a Microsoft Advertising blog post promoting a Microsoft Advertising webinar — a vendor/practitioner source with a commercial interest in this topic, not neutral research; treat prescriptive advice accordingly (see Evidence Quality on the article-summary page).
- ## Open Questions
	- The 357%/1.13B traffic-referral stat is attributed to TechCrunch/SimilarWeb but not independently re-verified from this ingest — worth ingesting the TechCrunch piece directly if this number matters for a real decision.
	- Almost all the structural/formatting advice (em-dash caution, bullet overuse, etc.) is asserted without citation or study — reads as plausible practitioner best-practice, not established evidence. Worth flagging rather than treating as settled.
	- Resolved 2026-08-23: yes, a real thread — [[mem/projects/geo-for-eot]] created, with the site audit as its first backlog item (not yet run).
