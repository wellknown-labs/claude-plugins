# Wellknown Workspaces

Your consulting workspaces in Claude, ChatGPT and Codex. Search a workspace's documents with
citations, run your firm's own playbooks, and have the assistant file the claims of its answer
for you to check.

## What it includes

- **Skills** that teach the assistant how to use Wellknown Workspaces well:
  - `using-workspaces`: open the conversation's binding first and let you choose the workspace;
    cite every fact from the data room; say what it could not see; add documents; recall and
    record what the team decided.
  - `search-data-room`: answer a question with cited evidence, and file the answer's claims.
  - `run-playbook`: load your firm's playbook live, follow it to the end, and propose changes
    to it.
- **A connection** to the Wellknown Workspaces MCP server, on ChatGPT and Codex. You sign in once,
  and approve the application once, on Wellknown's site.

## On Claude, add the connector too

On Claude this plugin ships **skills only**. The server reaches Claude as a connector, because a
server that arrives through a Claude plugin never renders Wellknown's apps (the workspace picker,
the Claims Panel, the upload panel; see anthropics/claude-ai-mcp#274). **The skills do nothing
without the connector.** The connector URL is `https://mcp.wellknownlabs.com/v1/mcp`.

An administrator adds it once for the organisation (claude.ai: **Organization settings →
Connectors**), or you add it yourself as a custom connector. In Claude Code, run
`claude mcp add --transport http workspaces <URL>`.

Wellknown Workspaces works without this plugin too: every tool is available to any MCP client at
the same URL. The plugin adds the guidance.

## Each conversation

The assistant asks Wellknown Workspaces for a binding at the start of each conversation.
- With one workspace, you can start straight away.
- With several, you choose which ones this conversation may use, in the picker the host shows or
  on a Wellknown page. The confirmation code on that page must match the one the assistant shows
  you.

The assistant can never choose a workspace for you.
