title:: templates/ctx/snippet
type:: template
tags:: system, template

- Starter for a new `ctx/snippets/` page.
- ---
- title:: {{title}}
  type:: snippet
  date:: {{date}}
  language:: markdown | python | javascript | mermaid | other
  use_case::
  tags::
- ## Code
	- ```{{language}}
	  The reusable code/text block.
	  ```
- ## Usage
	- *When and how to use this.*
- ## Source
	- [[raw/...]] —
