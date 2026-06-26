---
type: reference
title: "Claude Code: SOW-to-Jira Skill"
description: Claude Code skill and mcp-atlassian setup that converts an A17 features & requirements matrix (CSV or Confluence) into structured Jira Epics and Stories.
tags:
  - claude-code
  - reference
---
# Claude Code: SOW-to-Jira Skill

## What This Does

Reads a features & requirements matrix (from CSV or Confluence) and creates structured Jira Epics and Stories automatically. Built for the A17 workflow where SOW intake and Q&A happen first, resulting in a clean matrix that then needs to become tickets.

## How We Got Here

### The Problem
AREA 17 uses Confluence to store a refined features & requirements matrix extracted from SOWs and client Q&A. Turning that matrix into Jira tickets is manual and tedious -- copying feature names, descriptions, priorities, and phase info row by row.

### The Solution
A Claude Code skill (`sow-to-jira`) paired with the `mcp-atlassian` MCP server. The skill reads the matrix, maps columns to Jira fields, presents a plan for review, and creates all tickets on confirmation.

### Decisions Made

| Decision | Choice | Why |
|----------|--------|-----|
| Epic naming | Title Case | "DISCOVERY & STRATEGY" → "Discovery & Strategy" for readability |
| TBD scope items | Create with `tbd` label | Keeps them visible and tracked without committing |
| Optional scope items | Create with `optional` label | Same rationale -- visible but clearly flagged |
| Multi-phase items (Phase 1/2) | Apply both phase labels | `phase-1` + `phase-2` so they show up in either filter |
| Out of Scope items | Skip entirely | No tickets created, no Epic created |
| Notes column | Story description addendum | Added under a "Clarifications" header in each Story |
| Input source | CSV or Confluence | CSV is faster for spreadsheet exports; Confluence for live pages |

### Column Mapping (A17 CSV Format)

```
Column A: Features          → Epic (title-cased)
Column B: Requirements      → Story summary
Column C: Requirements Desc → Story description
Column D: Risk Level        → Jira Priority (High/Medium/Low)
Column E: Phase             → Labels (phase-1, phase-2, post-launch, ongoing)
Column F: In Scope          → Filter + Labels (Yes/No/TBD/Optional)
Column G: Notes             → Story description under "Clarifications"
Columns H+:                 → Ignored (spreadsheet artifacts)
```

### Scope Filtering

| In Scope Value | Action |
|----------------|--------|
| Yes / Yes (new) | Create ticket normally |
| No | Skip -- no ticket created |
| TBD | Create ticket with `tbd` label |
| Optional | Create ticket with `optional` label |

### Expected Output (from the NAE matrix)

- 17 Epics (excluding Out of Scope)
- ~89 Stories total
- 3 stories labeled `tbd`
- 2 stories labeled `optional`

---

## What Was Installed

### 1. MCP Server: `mcp-atlassian`

An open-source MCP server ([github.com/sooperset/mcp-atlassian](https://github.com/sooperset/mcp-atlassian), 4.5k stars) that gives Claude Code tools to read/write Confluence and Jira.

**Registered in:** `~/.claude.json` under `mcpServers`

**How it works:**
```
You → Claude Code → MCP server (local process on your machine) → Atlassian API → area17.atlassian.net
```

- Runs as a local subprocess, started automatically when Claude Code opens
- Your API token stays on your machine (passed as env var to the local process)
- Uses your Atlassian account permissions -- can only do what james@area17.com can do
- Claude Code asks permission before calling MCP tools

**Credentials configured:**
- Confluence: `https://area17.atlassian.net/wiki` (james@area17.com)
- Jira: `https://area17.atlassian.net` (james@area17.com)
- API token stored in `~/.claude.json` (not in any .env file)

**To update credentials later:** edit `~/.claude.json`, find the `mcpServers.mcp-atlassian.env` section.

**To remove:** `claude mcp remove mcp-atlassian`

### 2. Claude Code Skill: `sow-to-jira`

**Location:** `~/.claude/skills/sow-to-jira/`

```
sow-to-jira/
├── SKILL.md                      # Main skill instructions
├── SETUP.md                      # This file
└── references/
    └── parsing-patterns.md       # Parsing heuristics for different formats
```

---

## How to Run

### Prerequisites

1. **Restart Claude Code** after initial setup (MCP servers load on startup)
2. **Verify the MCP server is running:** look for `mcp-atlassian` in the server list when Claude Code starts
3. **Have a Jira project key** ready (e.g., `JS` from `https://area17.atlassian.net/jira/software/c/projects/JS/`)

### Step 1: Test Your Connection

Open Claude Code and type:

```
Create a test Story in project JS with summary "Test ticket - delete me"
```

If it works, you'll see a ticket key (e.g., `JS-123`). Delete it manually in Jira or ask Claude to delete it.

If it fails, check:
- Is the API token valid? (regenerate at https://id.atlassian.com/manage-profile/security/api-tokens)
- Does your account have permission to create issues in the JS project?
- Did you restart Claude Code after setup?

### Step 2: Run the Skill

#### From CSV (fastest)

```
sow to jira from /Users/jamesgillispie/Downloads/[INT] A17 + NAE Features & Requirements - Features & Requirements.csv into project JS
```

Or shorter:

```
csv to jira /path/to/file.csv project JS
```

#### From Confluence

```
sow to jira from https://area17.atlassian.net/wiki/spaces/SPACE/pages/12345/Page+Title into project JS
```

### Step 3: Review the Plan

Claude will parse the matrix and show you the proposed breakdown:

```
## Proposed Jira Structure for project JS

### Epic: Discovery & Strategy
Stories:
  1. Stakeholder Research (Medium, phase-1)
  2. Audience Research & Personas (Medium, phase-1)
  ...

This will create 17 Epics and 89 Stories in project JS.
3 items marked TBD (will get 'tbd' label)
2 items marked Optional (will get 'optional' label)

Confirm? (y/n)
```

Review, request changes, then confirm.

### Step 4: Tickets Created

Claude creates Epics first, then Stories linked under each Epic. You'll see a summary table when done:

```
| Epic | Key | Stories | Story Keys |
|------|-----|---------|------------|
| Discovery & Strategy | JS-1 | 7 | JS-2 through JS-8 |
| ...
```

---

## Safety Notes

- **Nothing is created until you confirm.** The skill always presents a plan first.
- **Claude Code asks permission** before calling Jira write tools.
- **Your API token = your permissions.** The tool can only do what your Atlassian account can do.
- **Test with a sandbox project first** if you're concerned about cluttering a production board.
- **To undo:** bulk-delete created tickets in Jira, or delete the entire test project.

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| MCP tools not available | Restart Claude Code. MCP servers load on startup. |
| "Authentication failed" | Regenerate API token at https://id.atlassian.com/manage-profile/security/api-tokens and update `~/.claude.json` |
| "Project not found" | Verify the project key at https://area17.atlassian.net/jira/projects |
| "Permission denied" on issue creation | Your Atlassian account needs "Create Issues" permission in the target project |
| CSV parsing wrong columns | The skill expects the A17 format (Features, Requirements, Requirements Desc, Risk Level, Phase, In Scope, Notes). If your CSV is different, tell Claude and it will ask you to map columns. |
| Epic already exists | The skill creates new Epics each run. If re-running, either use a different project or delete the previous Epics first. |

---

## Updating the Skill

The skill lives at `~/.claude/skills/sow-to-jira/SKILL.md`. Edit it directly to change behavior -- for example:
- Add new column mappings for different CSV formats
- Change default labels or priority mappings
- Adjust the confirmation flow

Changes take effect immediately in the next Claude Code session that loads the skill.
