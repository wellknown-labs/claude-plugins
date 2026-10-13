---
name: wellknown
description: Use when the user types /wellknown, mentions Wellknown, their data room, project files, claims or playbooks, or asks for analysis that should be grounded in their Wellknown project.
---

# The user has invoked Wellknown. Their request must be answered from their Wellknown project through the Wellknown connector, not from general knowledge and not from the web.

## Rule 1: the first action is a Wellknown tool call

Before writing any answer, plan, or web search, call a Wellknown tool. No exceptions, even if the request looks simple or you think you already know the answer.
1. Check your tool list for tools from the Wellknown connector (names containing "Wellknown", such as describe_workspace, search_knowledge, list_playbooks).
2. If they are not listed, they may be deferred. Search your tools for "Wellknown" and load them before doing anything else.
3. If no Wellknown tools exist after that search, stop. Tell the user in one line: "The Wellknown connector isn't on for this chat. Turn it on via + > Connectors > Wellknown, then send your request again." Do not answer the request without it.

## Rule 2: orient, then retrieve
1. Call describe_workspace (and describe_binding or open_binding if the conversation is not yet linked to a project) to confirm which project and data room you are working in. If several projects could match, ask the user which one.
2. If the request is a recognisable consulting task (due diligence, market scan, competitor analysis, etc.), call list_playbooks and, if one fits, get_playbook. Follow the playbook's steps, quality checks, tone and output style. The user's own instructions in this message take priority where they conflict.
3. Retrieve evidence with search_knowledge. Batch related questions into one call where possible. Use list_documents, get_document_outline, fetch_document and get_page_images when you need a specific file or page.
4. Use recall for project context such as earlier decisions or hypotheses.

## Rule 3: cite and report claims
- Cite every Wellknown-sourced fact inline with its visible claim ID (for example WK8241) where a footnote number would go.
- Whenever your reply contains WK IDs, call submit_claims afterwards with the headers used, the claim IDs used, and their position relative to those headers, so the Claims Panel can render.
- If the data room does not contain the answer, say so plainly. You may then offer web search or general knowledge, clearly labelled as not from Wellknown, and offer to log the gap with create_open_question or request_enrichment.

## Rule 4: stay on Wellknown for the rest of the task
Once invoked, keep using Wellknown for follow-up questions in the same task without the user having to repeat /wellknown. Save durable project context (new decisions, changed timelines, hypotheses the user states) with remember when the user asks for it.

# Never
- Never answer from general knowledge first and check Wellknown afterwards.
- Never run a web search before the Wellknown search.
- Never invent claim IDs or cite an ID that a Wellknown tool did not return.
