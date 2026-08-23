---
type: source
date: 2026-08-23
origin: "https://raw.githubusercontent.com/open-spaced-repetition/fsrs4anki/main/README.md"
media: article
tags: [spaced-repetition, anki, algorithm]
status: extracted
---

# FSRS4Anki — Extracted Knowledge Base Notes

> Extracted via WebFetch on 2026-08-23. This is a distilled extraction, not a
> verbatim copy of the source README — see `origin` for the primary source.

## 1. What FSRS Is & Core Problem Solved
FSRS4Anki is "a modern spaced-repetition scheduler for Anki based on the Free
Spaced Repetition Scheduler algorithm." It addresses the limitation of Anki's
built-in scheduler by employing a data-driven approach. The project "follows
the path pioneered by Maimemo: data-driven, balancing interpretability and
verifiability."

## 2. Differences from Older Algorithms (SM-2)
The source does not explicitly contrast FSRS with SM-2/SuperMemo. It notes
that "The Ease Factor is no longer relevant when FSRS is enabled" and "The
`New Interval` setting is no longer relevant when FSRS is enabled" —
implying FSRS abandons SM-2's ease-factor mechanism for a different model.

## 3. Underlying Model/Mechanism
FSRS has "two main parts: the scheduler and the optimizer." The optimizer
"uses machine learning to learn your memory patterns and finds parameters
that best fit your review history." Specific memory factors (difficulty,
stability, retrievability) are referenced by name elsewhere in this vault's
general knowledge but were **not** detailed in this particular source —
flagged as an open question below rather than filled in from outside it.

## 4. Named People Credited
- **Jarrett Ye** (GitHub: L-M-Sherlock) — FSRS research engineer at MaiMemo
- **Damien Elmes** — founder of Ankitects; provided "invaluable technical support"
- Contributors listed: Expertium, user1823, Christos Longros

## 5. Evidence, Benchmarks, Comparisons
No benchmark results or performance comparisons appear in this README. Two
academic papers are cited by title only, findings not summarized here:
- "A Stochastic Shortest Path Algorithm for Optimizing Spaced Repetition
  Scheduling" (KDD)
- "Optimizing Spaced Repetition Schedule by Capturing the Dynamics of
  Memory" (TKDE)

## 6. Practical Usage/Tools
- Primary platform: Anki 23.10+ (integrated); older versions via separate tutorial
- Companion tool: FSRS Helper add-on
- Add-on compatibility table: 13 add-ons listed (9 compatible, 4 incompatible)
- Users can share review data via a Google Form to help improve the model

## 7. Limitations/Open Issues (as stated in source)
- Incompatible with add-ons that affect a card's intervals (e.g. Delay
  Siblings, Auto Ease Factor, autoLapseNewInterval, Straight Reward)
- "FSRS was not designed for incremental reading"
- Requires Anki 23.10+ for the simplest setup

## 8. Related Concepts/Algorithms Referenced
- Awesome FSRS repository (implementations across languages, papers, examples)
- "Spaced Repetition Algorithm: A Three-Day Journey from Novice to Expert" (intro guide)
- Research notebooks with documented analyses/experiments
