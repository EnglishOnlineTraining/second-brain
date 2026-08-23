title:: templates/ctx/session
type:: template
tags:: system, template

- **Sessions no longer get their own page.** In the Logseq layout, a decision/session log is a block appended to **today's journal** (`journals/yyyy_MM_dd.md`), not a standalone `ctx/sessions/` page — that's what journals are for. Paste the block below into today's journal and fill it in.
- ---
- ## Session: {{title}} #decision
	- **Objective:** *What was the goal of this session?*
	- **Key Decisions**
		- **Decision:**
			- *Rationale:*
			- *Linked context:* [[wiki/concepts/...]]
	- **Insights Generated**
		-
	- **Action Items**
		- TODO
	- **Open Questions**
		-
	- **Artifacts Created**
		- [[output/...]] —
	- **Participants:** [[mem/people/...]]
	- **Context:** [[wiki/concepts/...]], [[mem/projects/...]]
