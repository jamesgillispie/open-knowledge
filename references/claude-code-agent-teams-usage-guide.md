---
type: reference
title: "Claude Code: Agent Teams Usage Guide"
description: "Guide to using Claude Code experimental Agent Teams: enabling the flag, building a team, keyboard controls, and the lead/teammate plan-approve-build workflow."
tags:
  - claude-code
  - reference
---
# Claude Code: Agent Teams Usage Guide

## Preparation

- Add `"CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"` to the `~/.claude/settings.json` file
- Write to the project folder CLAUDE.md (rules, file ownership, tech stack)
- Start Claude Code with the `claude` command
- Set the model with `/model claude-opus-4-6`

## Build the Team

- Tell Claude in natural language: "create an agent team, with these teammates"
- Specify to each teammate what they should do and which files they will edit
- Say "Require plan approval" — they should write a plan first, then you/lead approve it
- Say "Use Sonnet for teammates" — costs will be lower

## Controls

- Shift+Tab → opens delegate mode (lead doesn't write code, only coordinates)
- Ctrl+T → view the task list
- Shift+Up/Down → switch between teammates
- If you want to message a teammate directly, select them and type

## Workflow

- Lead creates and distributes tasks
- If there are dependencies (e.g. types.ts must be finished first), lead sets the order
- Teammate writes plan → lead approves → teammate writes code
- When teammate finishes, reports back to lead
- Lead collects and merges the results
