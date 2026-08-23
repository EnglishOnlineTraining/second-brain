---
name: ingest
description: Capture a source (URL, file path, or raw text) into the second-brain Logseq graph — save it to raw/, extract concepts/people/literature into pages/wiki-*.md pages, cross-link them, write a summary, and log the operation. Use whenever Shaun says "ingest <url>", "capture this", "add this to the knowledge base", or hands over an article/paper/note to file away.
---

# /ingest — Capture Source → Extract Knowledge

**Trigger:** User provides a URL, file path, or raw text.

**Usage**
```
/ingest <url-or-file-path> [tags...]
/ingest --batch <folder-path>
```

## Workflow

1. **Save to `raw/`**
   - If URL: fetch content, convert to clean markdown, save as `raw/articles/YYYY-MM-DD-{slug}.md`
   - If PDF: copy to `raw/pdf/YYYY-MM-DD-{slug}.pdf`, extract text to a `.md` alongside it — or save straight to `assets/` if the human will want to open/annotate it inside Logseq
   - If screenshot: save to `raw/screenshots/YYYY-MM-DD-{slug}.png`, add OCR text to `raw/notes/`
   - If voice: save to `raw/voice/`, transcribe to `raw/transcripts/`
   - Add a YAML metadata header to the raw file itself (this is plain file metadata, not a Logseq page — `raw/` is outside `pages/`):
     ```yaml
     ---
     type: source
     date: YYYY-MM-DD
     origin: "URL or file path"
     media: article | pdf | screenshot | voice | transcript | note
     tags: [tag1, tag2]
     status: unread | skimmed | read | extracted
     ---
     ```

2. **Read & Analyze**
   - Read the source completely.
   - Identify: key concepts, people mentioned, core claims, evidence/methodology, relevance to focus areas.
   - Rate evidence quality: strong | moderate | weak | anecdotal

3. **Extract to `pages/wiki-*`**
   - **New concepts:** Create `pages/wiki-concepts-{slug}.md` from `pages/templates-wiki-concept.md`. First block: `title:: wiki/concepts/{slug}` + properties. Fill Definition, Key Insights, Connections, Open Questions.
   - **New people:** Create `pages/wiki-people-{slug}.md` from `pages/templates-wiki-person.md`. `title:: wiki/people/{slug}`. Fill Role, Key Contributions, Positions.
   - **Literature entry:** Create `pages/wiki-literature-{slug}.md` from `pages/templates-wiki-literature.md`. Bibliographic data, key findings, your notes.
   - **Permanent note:** If the source sparks an original insight, create `pages/wiki-permanent-notes-YYYY-MM-DD-{slug}.md` linking source to your thinking.
   - **Update existing pages:** Read current version, append new insight blocks, update `updated::` property, add source to `sources::`.
   - **Cross-link pass:** Ensure every new page has ≥2 `[[references]]`. Add backlinks where concepts co-occur in block text — that's how Logseq builds Linked References.

4. **Write summary**
   - Create `pages/wiki-articles-YYYY-MM-DD-{slug}-summary.md` from `pages/templates-wiki-article-summary.md`, or a shorter `pages/wiki-references-{slug}.md` for a quick-reference entry.
   - One-line essence + key arguments + concepts introduced + follow-up questions

5. **Log**
   - Append to `log.md`:
     ```markdown
     ## YYYY-MM-DD HH:MM
     - **Operation:** ingest
     - **Source:** `raw/...`
     - **Pages created:** [[wiki/concepts/...]], [[wiki/people/...]]
     - **Pages updated:** [[wiki/concepts/...]]
     - **Literature:** [[wiki/literature/...]]
     - **Permanent note:** [[wiki/permanent-notes/...]] (if any)
     - **Evidence quality:** strong | moderate | weak
     - **Notes:** Anomalies, human attention needed
     ```
   - Also append a short block to today's `journals/yyyy_MM_dd.md`, e.g. `- #ingest [[wiki/concepts/...]] from [[raw/articles/...]]`, so the capture shows up natively in Logseq too.

6. **Update index**
   - Refresh `pages/wiki-index.md` if new categories or major pages added.

## Output
Report: source saved, pages created/updated, evidence quality, any flags.
