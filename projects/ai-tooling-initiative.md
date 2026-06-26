---
type: project
title: AI Tooling / Internal Agent Initiative
description: "AREA 17's grassroots AI adoption: Claude/Cursor skills, internal dashboards, regression audits, BD automation, and agentic QA."
tags:
  - project
  - area-17
---
# AI Tooling / Internal Agent Initiative

A rapid, largely grassroots wave of AI adoption inside [AREA 17](/clients/area-17/overview.md), spanning everyday tooling, shared skills, and early agentic concepts. The umbrella theme is [AI Tooling Adoption & Agent Harnessing](/concepts/ai-tooling-adoption.md); a formal AI working group is being reinstated as part of the [transformation](/projects/a17-transformation.md).

## Status

Active. Everyday tooling is in real use; agentic concepts (purpose-built agents, agentic QA) are in prototyping/trial.

## What's in use

- **[Nikki](/people/nikki.md)'s Jira-connected analytics dashboard** built with Claude (shared with a client as PDF exports as a workaround), plus FigJam-style breakdowns. Path forward: use Claude's co-work scheduler to auto-refresh and output static HTML, plus a weekly plain-language digest email.
- **Pablo's Twill/Laravel skill for Claude/Cursor** — takes a navigation/CMS structure definition and generates migrations, capsule scaffolding, etc. Next step is moving toward an agent model with proper validation gates, not just unit tests.
- **Shared, versioned skills** — skills live in a repo where team members submit MRs; **mpx-skills** (an NPM-based skills manager) sync-links skills to Claude/Cursor and checks for updates. Antonio's complementary approach uses project-level `.claude.md` / `AGENT.md` files pointing at per-framework rule files.
- **Claude Opus release-branch regression audits** — Opus used to audit a giant release branch for regressions before merging; it caught real issues, flagged to the team, fixed before merge. See [Release Engineering](/concepts/release-engineering.md).
- **Claude-generated Jira tickets** — cleaner and more detailed than manual entry.

## Concepts in prototyping

- **James's single-purpose 'minion' / harness agent** — a README bot with its own repo user account, triggered via commit message (e.g. `@a17-readme-bot update readme`), deterministic scope (only updates READMEs), inspired by Stripe's "minions" pattern of purpose-built agents with explicit success/failure outputs.
- **Agentic Playwright QA** — humans describe tests, AI implements, humans verify; a fixed bug's test stays in the suite permanently as a regression test. Extended vision: a dedicated QA agent with its own email, Jira, GitLab, and CMS credentials that gets @-mentioned, recreates the bug, and drafts an MR — governed like a team member whose access can be revoked.
- **Claude Tag Slack BD-automation** — a HubSpot entry triggers Slack BD-channel creation, a Drive folder, Scoro placeholders, and an automatic site audit, with Claude Tag routing brand vs. technical work to the right people.

## Governance model

AI use follows an **internal-first principle** (prove it on AREA 17's own work before client-facing use) and an **access-revocation model** — agents are treated like team members added to a project, controllable by revoking their credentials. Human review (PR/MR gates) is required before any agent output reaches a codebase.

## Key decisions

- **Trial Anthropic's Claude Tag Slack integration** (using $2,500 in free credits) as the BD-automation / routing layer, chosen because it stays inside the existing Slack/Claude ecosystem — rather than Dobbin (~$5k/mo for the needed tier).
- **Disable Microsoft Clarity's default content masking per project** — Clarity was masking content (and images), severely on healthcare projects, via AI-based sensitivity detection. Audit and unmask [Pentagram](/clients/pentagram/overview.md), [National Academies](/clients/nasem/overview.md), and VMFA first; check all accounts.

## People

- [James Gillispie](/people/james-gillispie.md) — driving the agent/harness concepts and AI direction.
- [Nikki](/people/nikki.md) — dashboards and analytics tooling.
- [Citrine](/people/citrine.md) — ops; part of the governance/check-in loop.

## Organization

[AREA 17](/clients/area-17/overview.md)
