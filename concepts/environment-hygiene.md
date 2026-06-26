---
type: concept
title: "Environment Hygiene: Pre-Prod & QA Workflow"
description: A dedicated client-QA pre-prod environment and cleaner bug-reporting workflow to kill false bugs.
tags:
  - concept
  - theme
---
# Environment Hygiene: Pre-Prod & QA Workflow

A recurring proposal to eliminate a whole class of wasted effort: false bugs caused by content and configuration drift between environments, and the messy QA workflow around them.

## The core proposal

Stand up a **dedicated client-QA pre-prod environment**:

- **Cloned from production** so it matches real content and config.
- **Synced per release** so it stays current with each deployment.
- **"Pencils down" for the client** — the client tests against this stable, synced environment instead of a moving target, so the bugs they file are real rather than artifacts of drift.

The payoff is killing content/config-drift false bugs — issues that look like defects but are really just the test environment being out of sync with production.

## Supporting workflow improvements

- **A cleaner Jira workflow** so issues move through clear, unambiguous states.
- **Screen-recorded bug reproductions** via tools like Jam.dev or Loom, so a reported bug carries the exact reproduction rather than a vague description.

## Reference point

[Pentagram](/clients/pentagram/overview.md) is cited as the reference for how this should work — the model to emulate.

## Where it applies

The [NASEM Site](/projects/nasem-site.md) is the leading case where drift-driven false bugs and QA friction made the need acute.

## Why it recurs

Without a synced pre-prod, every release invites the same waste: time spent triaging "bugs" that are really environment mismatches. It connects to [Sprint vs. Retainer Model for Complex Platforms](/concepts/sprint-vs-retainer.md) and [Release Engineering: Large Multi-Branch Merges](/concepts/release-engineering.md) — environment hygiene is what keeps fast release cadences from drowning in false defects.

## Through-line

Give the client a stable, prod-cloned, per-release-synced place to test, with crisp Jira states and recorded repros — and most "bugs" disappear before they cost anyone time.