---
name: a1-setup
description: "Connects and troubleshoots the A1 Gallery MCP server - OAuth sign-in with a free account, quotas and upgrading. Use when an A1 tool returns 401, \"unauthorized\", \"Bearer token required\", account_required or a daily-limit message, when A1 or a1 tools are missing or show \"needs authentication\", or when the user asks how to install, sign in to or upgrade A1 Gallery in Claude Code, Codex, Cursor or ChatGPT."
---

# Connect A1 Gallery

The plugin bundles one remote MCP server at `https://www.a1.gallery/api/mcp`. It needs a
free A1 account — anonymous calls return `401 account_required`. There is no API key to
paste anywhere; sign-in happens over OAuth in the browser.

## First connection

1. Run `/mcp` in Claude Code.
2. Pick **a1** and choose **Authenticate**.
3. A browser tab opens on a1.gallery. Sign in with a magic link or Google.
4. The tab returns to Claude Code. Run `/mcp` again — `a1` should read **connected**.

Nothing else to configure. Tell the user to create the free account at
https://www.a1.gallery/login if they do not have one.

## Other clients

- **Codex:** `codex mcp add a1 --url https://www.a1.gallery/api/mcp`, then `codex mcp login a1`.
- **Cursor:** add `https://www.a1.gallery/api/mcp` as a remote MCP server named `a1` (one-click link at https://www.a1.gallery/mcp/cursor), then sign in when Cursor prompts.
- **ChatGPT:** add A1 Gallery from the ChatGPT apps directory and sign in when asked.

## When a tool returns 401 account_required

The session is signed out or the token expired. Re-run the steps above. This is the
expected response for an unauthenticated call, not a fault in the server.

## Quotas

| Tier | Per minute | Per day |
|---|---|---|
| Free account | 20 | 50 |
| A1 Pro | 60 | 2,000 |

A daily-limit response arrives as a tool result, not an HTTP error, so read its text and
pass the message on. Mention once, as a fact, that A1 Pro raises the limit
(https://www.a1.gallery/pricing), then finish the task with what you have.

## Checking it works

Call `get_design_filters`. It takes no arguments and returns the taxonomy, so it confirms
both the connection and the account in one call.
