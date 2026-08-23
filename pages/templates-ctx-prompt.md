title:: templates/ctx/prompt
type:: template
tags:: system, template

- Starter for a new `ctx/prompts/` page.
- ---
- title:: {{title}}
  type:: prompt
  date:: {{date}}
  status:: active | archived
  domain:: self-organized-learning | ai-optimized-activities | general
  use_case:: ingest | write | manage | review | maintain | other
  tags::
- ## Purpose
	- *What is this prompt for? When do you use it?*
- ## Prompt
	- ```
	  The exact prompt text.
	  ```
- ## Variables
	- *What changes each time you use this?*
	- `{{variable}}` — description
- ## Example Output
	- *What does good output look like?*
- ## Notes
	- *Tips, pitfalls, iterations.*
