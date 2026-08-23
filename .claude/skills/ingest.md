# /ingest

Capture raw source material, extract knowledge, and add it to the wiki.

## Usage
```
/ingest <url-or-file-path> [tags...]
/ingest --batch <folder-path>
```

## Workflow

1. **Save to raw/**
   - If URL: fetch content, convert to clean markdown, save as `raw/articles/YYYY-MM-DD-{slug}.md`
   - If PDF: copy to `raw/pdf/YYYY-MM-DD-{slug}.pdf`, extract text to `.md` alongside it
   - If screenshot: save to `raw/screenshots/YYYY-MM-DD-{slug}.png`, add OCR text to `raw/notes/`
   - If voice: save to `raw/voice/`, transcribe to `raw/transcripts/`
   - Add source frontmatter:
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

3. **Extract to wiki/**
   - **New concepts:** Create `wiki/concepts/{slug}.md` from template. Fill Definition, Key Insights, Connections, Open Questions.
   - **New people:** Create `wiki/people/{slug}.md` from template. Fill Role, Key Contributions, Positions.
   - **Literature entry:** Create `wiki/literature/{slug}.md` with bibliographic data, key findings, your notes.
   - **Permanent note:** If the source sparks an original insight, create `wiki/permanent-notes/YYYY-MM-DD-{slug}.md` linking source to your thinking.
   - **Update existing pages:** Read current version, append new insights, update `updated` date, add source to `sources` list.
   - **Cross-link pass:** Ensure every new page has ≥2 `related` links. Add backlinks where concepts co-occur.

4. **Write summary**
   - Create `wiki/articles/YYYY-MM-DD-{slug}-summary.md` or `wiki/references/{slug}.md`
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

6. **Update index**
   - Refresh `wiki/index.md` if new categories or major pages added.

## Output
Report: source saved, pages created/updated, evidence quality, any flags.
