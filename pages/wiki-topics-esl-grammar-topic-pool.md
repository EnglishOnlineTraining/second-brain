title:: wiki/topics/esl-grammar-topic-pool
type:: topic
created:: 2026-08-23
updated:: 2026-08-23
status:: draft
sources:: [[raw/notes/2026-08-23-esl-grammar-topic-pool]]
related:: [[mem/projects/geo-for-eot]]
tags:: esl, grammar, curriculum, keyword-research

- ## Overview
	- A ranked pool of ESL grammar topics, tiered by triangulating three independent evidence streams: search demand (SpyFu/Google Trends/ELL Stack Exchange), learner-error frequency (NUCLE, Cambridge Learner Corpus, TOEFL11, ICLE, NICT JLE + named error-analysis studies), and teaching attention (Murphy/*Azar* unit counts, British Council engagement, engVid views). Topics land in Tier 1 (all three streams agree), Tier 2 (two streams, or one very strong), or Tier 3 (consistently popular / level- or L1-specific). Directly relevant to how [[mem/claude]]'s two focus areas meet real curriculum work — this is exactly the kind of evidence base that should inform grammar-topic selection for an ESL activities site.
- ## Key Concepts
	- **The "Big Eight" (Tier 1):** tense system as a whole, present perfect (vs. past simple), articles, prepositions, subject–verb agreement, conditionals, passive voice, modal verbs — full evidence for each in [[raw/notes/2026-08-23-esl-grammar-topic-pool]].
	- **The "stable Big Five" of learner pain** (the source's own cross-cutting finding): articles, prepositions, tense/aspect, subject–verb agreement, and noun countability account for the majority of errors across every corpus surveyed.
	- **L1-specific error patterns:** article-less L1s (Chinese/Japanese/Korean, Slavic, Turkish, Thai) → 3–4× more article errors; Arabic L1 → copula omission, double negatives, perfect-tense misuse; Romance L1s → perfect-tense overuse, preposition transfer; Chinese L1 → adverb placement, subject omission, relative-clause resumption.
- ## Key People
	- None named as individuals in the source — it cites corpora (NUCLE, Cambridge Learner Corpus, TOEFL11, ICLE, NICT JLE) and specific studies by author+year (Rozovskaya & Roth 2010, Han/Chodorow/Leacock 2006, Bitchener 2005, Dalgish 1985) rather than profiling researchers. Worth creating `wiki/people/` entries later if any of those studies get ingested directly.
- ## Key Literature
	- The underlying corpora/studies aren't ingested themselves yet — only cited within this compiled document. If any of Rozovskaya & Roth (2010), Han/Chodorow/Leacock (2006), Bitchener (2005), or Dalgish (1985) get ingested directly, link them here as `[[wiki/literature/...]]`.
- ## Current State
	- This is a compiled/secondary source (triangulated by the author, not a primary study) — well-methodology-described and internally consistent, but none of its individual figures (search volumes, corpus percentages, comment counts) have been independently re-verified in this ingest. The document itself flags its own main caveat: keyword volumes are US-market only; global demand (India, Pakistan, Philippines especially) is typically several times higher — and several Tier 2/3 entries explicitly note India/Pakistan curriculum-driven search spikes (e.g. "reported speech class 9", "SVA class 10").
- ## Opportunities
	- **Directly actionable for `vocab-games`:** that repo already runs a rigorous topic-pool system (`topic-pool.json`, the `add-topics`/`daily-exercise-draft` skills) for Year 8/10/MSA grammar-exercise selection, and separately runs SEO-targeted `themen/` German landing pages for specific grammar topics (e.g. "Passiv Englisch Übungen", "if-Sätze Klasse 10"). This pool's Tier 1/2 rankings — and especially its India/Pakistan curriculum-search-spike finding — is a genuine, evidence-based input for prioritizing *which* grammar topics get new exercises or dedicated `themen/` pages next, distinct from (but complementary to) the Klett-textbook-driven topic pools already in place there. Not acted on yet — flagged here for Shaun to decide whether it's worth feeding into that process.
	- Also complements [[mem/projects/geo-for-eot]]: search-demand data (which grammar topics people actually search for) is a content-strategy input alongside that project's structural/GEO-formatting checklist.
