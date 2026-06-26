---
type: reference
title: Atlassian MCP Setup — What We Built
description: Overview of the sow-to-jira Claude Code skill and mcp-atlassian server that convert SOW requirements matrices into Jira Epics and Stories.
tags:
  - research
  - atlassian
  - mcp
  - jira
  - sow-to-jira
source_url: https://github.com/sooperset/mcp-atlassian
---
# Atlassian MCP Setup — What We Built

## Summary

Set up a Claude Code skill and MCP server integration to automate converting SOW features/requirements matrices into structured Jira Epics and Stories. Eliminates the manual row-by-row ticket creation grind.

## Components

### 1. mcp-atlassian MCP Server

An open-source MCP server ([sooperset/mcp-atlassian](https://github.com/sooperset/mcp-atlassian)) registered at user scope in `~/.claude.json`. Gives Claude Code direct read/write access to Jira and Confluence via the Atlassian REST API.

- **Transport:** stdio via `uvx mcp-atlassian`
- **Scope:** User-level (available in all projects)
- **Auth:** Atlassian API token (email + token, Basic auth)
- **Targets:** `https://area17.atlassian.net` (Jira) and `https://area17.atlassian.net/wiki` (Confluence)

How it works:

```
You → Claude Code → MCP server (local subprocess) → Atlassian REST API → area17.atlassian.net
```

The server runs locally on your machine. API token stays local, passed as an environment variable. Permissions match whatever james@area17.com can do in Atlassian.

### 2. sow-to-jira Skill

A Claude Code skill at `~/.claude/skills/sow-to-jira/` that handles the parsing logic and ticket creation workflow.

**File structure:**

```
sow-to-jira/
├── SKILL.md                          # Main skill instructions
├── SETUP.md                          # Setup & usage guide with troubleshooting
└── references/
    ├── parsing-patterns.md           # Parsing heuristics for different source formats
    ├── jira-fields.md                # Jira field mapping reference
    └── confluence-jira-expansion.md  # Confluence-specific extraction patterns
```

### 3. Column Mapping System (A17 CSV Format)

The skill expects the A17 features & requirements matrix format:

| CSV Column | Jira Field |
|-----------|------------|
| Features (A) | Epic name (title-cased) |
| Requirements (B) | Story summary |
| Requirements Desc (C) | Story description |
| Risk Level (D) | Priority (High/Medium/Low) |
| Phase (E) | Labels (phase-1, phase-2, post-launch, ongoing) |
| In Scope (F) | Filter + Labels |
| Notes (G) | Description addendum under "Clarifications" |

Non-standard CSV formats (like the JS Technical Requirements file with extra columns for Type, Tech Domain, Complexity, Dependencies, Acceptance Criteria) are detected and the skill asks you to confirm mapping before proceeding.

### 4. Scope Filtering Logic

| In Scope Value | Action |
|---------------|--------|
| Yes / Yes (new) | Create ticket normally |
| No | Skip entirely — no ticket, no Epic |
| TBD | Create ticket with `tbd` label |
| Optional | Create ticket with `optional` label |

The "OUT OF SCOPE ITEMS" feature group is always skipped entirely.

### 5. Workflow

1. **Input** — provide a CSV file path or Confluence page URL, plus the target Jira project key
2. **Parse** — skill extracts features (Epics) and requirements (Stories), maps columns, applies scope/phase logic
3. **Plan** — full breakdown presented for review before anything is created
4. **Confirm** — you approve, modify, or reject the plan
5. **Create** — Epics created first, then Stories linked under each Epic
6. **Report** — summary table with all ticket keys

## Current Status

As of 2026-03-12, the MCP server is configured and reports `✓ Connected` via `claude mcp list`, but the Jira/Confluence tools are not being injected into Claude Code sessions. The skill and parsing logic work — the blocker is the MCP tool availability. See [Atlassian API Discovery — Rovo vs REST API](/references/atlassian-api-rovo-vs-rest.md) for troubleshooting notes.
