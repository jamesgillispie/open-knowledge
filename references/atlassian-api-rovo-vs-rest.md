---
type: reference
title: Atlassian API Discovery — Rovo vs REST API
description: Why the standard Atlassian REST API (not Rovo) is the right tool for the sow-to-jira workflow, plus MCP tool-loading troubleshooting.
tags:
  - research
  - atlassian
  - mcp
  - jira
  - api
---
# Atlassian API Discovery — Rovo vs REST API

## Context

While setting up the sow-to-jira integration (CSV → Jira Epics & Stories), the question came up about whether the Rovo API was needed. Short answer: no. They're different things.

## Standard Atlassian REST API

This is what the `mcp-atlassian` MCP server uses.

- **Purpose:** CRUD operations on Jira issues, Confluence pages, projects, users, etc.
- **Auth:** API token (email + token via HTTP Basic auth)
- **Token generation:** https://id.atlassian.com/manage-profile/security/api-tokens
- **Endpoints:** `https://<instance>.atlassian.net/rest/api/3/` (Jira), `https://<instance>.atlassian.net/wiki/rest/api/` (Confluence)
- **Use cases:** Create/update/search issues, read/write pages, manage projects, bulk operations
- **Rate limits:** Standard Atlassian Cloud limits (varies by endpoint)

This is the standard, well-documented API that's been around for years. It's the right tool for programmatic ticket creation.

## Rovo API

Atlassian Rovo is their AI platform — a separate product layer on top of Jira/Confluence.

- **Purpose:** AI-powered search, knowledge graph, AI agents that operate inside Atlassian
- **Auth:** OAuth 2.0 / Forge apps / Rovo Agent API keys (different from REST API tokens)
- **Use cases:**
  - Build AI agents that team members interact with in Jira/Confluence
  - AI-powered search across all Atlassian products
  - Knowledge retrieval and recommendations
  - Custom AI workflows within the Atlassian ecosystem
- **Not needed for:** Creating issues, reading pages, or any standard CRUD operations

## Key Differences

| | Standard REST API | Rovo API |
|--|------------------|----------|
| Auth | API token (Basic) | OAuth 2.0 / Forge / Agent keys |
| Operations | CRUD on issues, pages, projects | AI search, agents, knowledge graph |
| Maturity | Stable, well-documented | Newer, evolving |
| Needed for sow-to-jira | Yes | No |

## Current MCP Integration Status

The `mcp-atlassian` server is configured at user scope in `~/.claude.json` using the standard REST API approach:

- **Server:** `uvx mcp-atlassian` (stdio transport)
- **Credentials:** james@area17.com + API token
- **Targets:** area17.atlassian.net (Jira) and area17.atlassian.net/wiki (Confluence)
- **Health check:** Reports `✓ Connected` via `claude mcp list`

### The Problem

Despite the server showing as connected, the Jira/Confluence tools (e.g., `jira_create_issue`, `jira_search`, `confluence_get_page`) are not being injected into Claude Code sessions. The server process is running but its tools aren't reaching the model.

### Possible Causes

1. **Tool enumeration failure** — the server connects but fails to register its tools, possibly due to an auth validation error on startup against the Atlassian API
2. **Package version drift** — `uvx` runs the latest published version of `mcp-atlassian` each time; a breaking update may have landed since the original setup
3. **Tool permission gating** — Claude Code may require explicit approval of MCP tools on first use; there might be a prompt in the CLI that needs attention
4. **Token expiration** — Atlassian Cloud API tokens can expire; verify at https://id.atlassian.com/manage-profile/security/api-tokens

### Troubleshooting Steps

1. Check for tool approval prompts when starting a new Claude Code session
2. Test the server directly: `uvx mcp-atlassian --help`
3. Pin the package version to avoid drift: `uvx mcp-atlassian==2.5.0`
4. Check Claude Code logs for MCP-related errors (ctrl+p in CLI)
5. Remove and re-add the server with a fresh API token:

```bash
claude mcp remove mcp-atlassian -s user
claude mcp add -s user \
  -e CONFLUENCE_URL=https://area17.atlassian.net/wiki \
  -e CONFLUENCE_USERNAME=james@area17.com \
  -e CONFLUENCE_API_TOKEN=<new-token> \
  -e JIRA_URL=https://area17.atlassian.net \
  -e JIRA_USERNAME=james@area17.com \
  -e JIRA_API_TOKEN=<new-token> \
  mcp-atlassian -- uvx mcp-atlassian
```

## Security Note

The API token was exposed in terminal output during this session. Recommend rotating the token at https://id.atlassian.com/manage-profile/security/api-tokens and updating `~/.claude.json` with the new value.

## Bottom Line

Rovo is Atlassian's AI layer — irrelevant for the CSV-to-Jira ticket creation workflow. The standard REST API + API token is the correct setup. The current blocker is getting the MCP server's tools to load into Claude Code sessions, not an API type issue.

See also: [Atlassian MCP Setup — What We Built](/references/atlassian-mcp-setup-overview.md).
