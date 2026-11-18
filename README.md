# Syntra MCP server

The official remote MCP server of [Syntra](https://syntra.tymko.tech/en/), project management for teams and project offices.

Connect Claude, ChatGPT, Claude Code or any MCP client to your Syntra workspace. Ask about projects, tasks, risks and sprints in plain language, and, where your workspace allows it, let the assistant create and update them. The assistant acts with the same permissions as the person who connected it.

This repository holds the connection guide and the registry entry. The server is hosted by the Syntra team; there is nothing to install or run.

| | |
|---|---|
| Endpoint | `https://syntra.tymko.tech/mcp` |
| Transport | Streamable HTTP |
| Auth | OAuth 2.1 with PKCE; access keys (`Authorization: Bearer syn_…`) for clients that send headers |
| Registry | `io.github.Syntra-Tymko/syntra` in the [official MCP Registry](https://registry.modelcontextprotocol.io) |
| Full guide | https://syntra.tymko.tech/connectors/ |

## Requirements

- A Syntra account in a workspace on a paid plan (14-day free trial, no card: https://syntra.tymko.tech/en/). Reading works on every paid plan; writing is switched on per workspace on the plans that include it. See [pricing](https://syntra.tymko.tech/en/#pricing).
- An MCP client that supports remote servers.

## Connect

**Claude** (web, Desktop, mobile): Settings → Connectors, search for **Syntra**, click Connect, sign in to Syntra, pick the workspace and click Allow.

**Claude Code**

```bash
claude mcp add --transport http syntra https://syntra.tymko.tech/mcp
```

Then run `/mcp` to sign in.

**ChatGPT**: Settings → Apps → Add custom MCP server, URL `https://syntra.tymko.tech/mcp`, authentication OAuth. Sign in to Syntra and click Allow.

**Other clients**: point them to `https://syntra.tymko.tech/mcp` with OAuth, or send a Syntra access key as `Authorization: Bearer syn_…`. If you belong to several workspaces and want one connector per workspace, use the workspace's own address `https://syntra.tymko.tech/mcp/<workspace>` from Syntra → Settings → API.

## Tools

Read tools come with every connection. Write tools appear only when the workspace has writing switched on and you allowed "read and write" on the consent page. No tool can delete anything.

| Tool | What it does |
|---|---|
| `list_projects` | Projects you can see, with status, progress, deadline, health lights and open risks |
| `get_project` | One project in full: budget, health lights, tasks and risks |
| `list_tasks` | Tasks across projects, filtered by project, status, assignee, sprint or date |
| `get_task` | One task in full: description, checklist, latest comments |
| `list_sprints` | Sprints per department with dates, status and Story Points |
| `get_sprint` | One sprint in full: goal, tasks, burndown |
| `whoami` | Which user, workspace and role the connection acts as |
| `create_task` | Creates a task or a bug report (write) |
| `update_task` | Changes a task's fields (write) |
| `add_task_comment` | Comments on a task (write) |
| `add_checklist_items` | Adds checklist steps (write) |
| `set_checklist_item` | Ticks, unticks or renames a checklist step (write) |
| `create_project` | Creates a project (write) |
| `update_project` | Changes a project's fields, health lights or budget (write) |
| `add_risk` | Registers a risk with severity and mitigation (write) |
| `update_risk` | Changes, closes or reopens a risk (write) |

## Example prompts

- "Which projects need my attention this week?"
- "What is blocking the store opening project? Show the risks."
- "Move the ERP go-live to Friday and add a supply risk."

## Security and privacy

- The assistant sees only what the connected user can see; every call runs with that user's role.
- You can disconnect at any time in Syntra (Settings → API) or in your client.
- Customer data is stored and processed in the EU (Fly.io, Frankfurt; Cloudflare R2, EU jurisdiction).
- Report a vulnerability or ask for help: support@tymko.tech

## License

The documentation in this repository is under the MIT License. The Syntra service itself is proprietary.
