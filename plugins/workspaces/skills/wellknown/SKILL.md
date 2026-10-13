---
name: wellknown
description: Use when the user types /wellknown, mentions Wellknown, their data room, their workspace (they may call it a project) or its documents, claims or playbooks, or asks for analysis that should be grounded in their Wellknown workspace.
---

# The user has invoked Wellknown. Their request must be answered from their Wellknown workspace through the Wellknown connector, not from general knowledge and not from the web.

## Rule 1: the first action is a Wellknown tool call

Before writing any answer, plan, or web search, call a Wellknown tool. No exceptions, even if the
request looks simple or you think you already know the answer.
1. Check your tool list for tools from the Wellknown connector, such as `open_binding`,
   `describe_workspace`, `search_knowledge` and `list_playbooks`. In some apps their names also
   contain "Wellknown".
2. If they are not listed, they may be deferred. Search your tools for "Wellknown" and load them
   before doing anything else.
3. If no Wellknown tools exist after that search, stop. Tell the user in one line: "The Wellknown
   connector isn't on for this chat. Turn it on in this app's connectors, then send your request
   again." Do not answer the request without it.

## Rule 2: open the binding, orient, then retrieve

1. Call `open_binding` first, once per conversation, as `using-workspaces` describes, and pass its
   `binding` on every other call. Only the user chooses which workspaces this conversation may
   reach. If several could match the request, ask the user which one.
2. Call `describe_workspace` to confirm which workspace and data room you are working in.
3. If the request is a recognisable consulting task (due diligence, market scan, competitor
   analysis, etc.), follow `run-playbook`: call `get_playbook` with an `intent` saying what the work
   is (`list_playbooks` shows which playbooks exist). Follow the playbook's steps, quality checks,
   tone and output style, or the firm's `general_instructions` when no playbook matches. The user's
   own instructions in this message take priority where they conflict.
4. Retrieve evidence with `search_knowledge`, following `search-data-room`. Batch related questions
   into one call where possible. Use `list_documents`, `get_document_outline` and `fetch_document`
   when you need a specific document or section, and `get_page_images` to look at a page yourself.
   When the user asks to see pages, use `show_pages`.
5. Use `recall` for workspace context such as earlier decisions or hypotheses.

## Rule 3: cite, then file the claims

- Cite every Wellknown-sourced fact with the citation of the passage it came from, as
  `search-data-room` describes.
- When your reply answers a specific factual question, or drafts a deliverable the user asked for,
  file its claims in this order: write one sentence that states the answer, call `submit_claims`
  straight after it, then write the full answer below its result. Give each claim its honest
  `provenance`, its `citation_ids` when it comes from the data room, and the headings above it in
  your reply (`section_path`), so the Claims Panel can show it in place. `search-data-room` says
  which statements become claims.
- If the data room does not contain the answer, say so plainly, log the gap with
  `create_open_question` saying what is missing, and tell the user you did. You may then offer web
  search or general knowledge, clearly labelled as not from Wellknown.

## Rule 4: stay on Wellknown for the rest of the task

Once invoked, keep using Wellknown for follow-up questions in the same task without the user having
to repeat /wellknown. Save durable workspace context (new decisions, changed timelines, hypotheses
the user states) with `remember` when the user asks for it.

# Never

- Never answer from general knowledge first and check Wellknown afterwards.
- Never run a web search before the Wellknown search.
- Never invent a citation or a claim, or cite an id that a Wellknown tool did not return.
