---
type: thesis
title: Sprints can't build complex platforms
description: Time-boxed sprints structurally fail deeply-interdependent platforms; they need a retainer / lead-dev model. AREA 17's commercial default is mismatched to its hardest work.
status: open
confidence: 60
opened: 2026-06-26
horizon: 2026-12-31
tags:
  - thesis
  - engagement-model
  - area-17
  - contested
---
# Sprints structurally can't build complex platforms — and we keep selling sprints anyway

> [!WARNING] Thesis under test — contested by current practice
> **Status:** open · **Confidence:** 60% · **Opened:** 2026-06-26 · **Next review:** 2026-12-31
>
> This is the bet I hold that my own firm's commercial model resists. That tension is the point of tracking it.

## The bet

**Time-boxed sprint engagements structurally fail deeply-interdependent platforms.** The genuinely hard work — API sync, search relevance, integrations — gets back-loaded to the moment with the least slack, compounding regressions and QA load. Such platforms need a **retainer / dedicated lead-dev model**, and AREA 17's commercial default (sprints; care budgets converted into six-week sprints) is mismatched to its hardest engagements.

## Why I believe it

The pattern is documented in the concept and confirmed, live, in the recaps:

- [Sprint vs. Retainer Model for Complex Platforms](/concepts/sprint-vs-retainer.md): sprints front-load the visible work and back-load the risky, interdependent work; [NASEM](/projects/nasem-site.md) is the clearest case of hard pieces arriving at sprint-end. The downstream symptoms are [Release Engineering: Large Multi-Branch Merges](/concepts/release-engineering.md) and [Environment Hygiene](/concepts/environment-hygiene.md).
- The [Jun 15–19 recap](/notes/weekly/2026-06-20-recap.md) states it plainly: Nascent "really needs a **full-time retainer lead dev** rather than sprint-based work," with a ~30-branch release behaving like "a fourth full launch, with hard problems piling up at the end."

## The contradiction worth naming

The work shape pulls toward retainers; the **commercial pull goes the other way**. Sprints are easy to scope and easy to sell, so in the same week the lesson lands, NASAM's and Pentagram's remaining **$80k care budgets are being converted into six-week sprints** ([recap](/notes/weekly/2026-06-20-recap.md)) — the exact cadence the concept says doesn't fit the work. Believing this thesis and acting on it are two different things, and right now the firm is doing the second.

## What would change my mind

- The converted NASAM/Pentagram six-week sprints **ship cleanly** — no late-stage crunch, no regression spike — showing a well-run sprint *can* hold a complex platform.
- A retainer-run platform shows the *same* late-stage crunch, proving the cadence was never the cause (people/process was).
- The commercial reality is simply dominant: clients won't buy retainers, so the question is moot and the right move is to make sprints survivable, not replace them.

## Scorecard

- **2026-06-26** — Opened at 60%. Lower confidence than the others *on purpose*: the engineering evidence is strong, but the bet is really a claim about the **commercial model**, where I have less control and the counter-pressure is real. The converted care-budget sprints are the natural experiment — watch them.

## What this feeds

How 2027 care budgets get scoped, and a possible internal argument to [George](/people/george-a17.md) about matching engagement model to work shape — part of the broader [AREA 17 transformation](/projects/a17-transformation.md) and the [margin / over-servicing](/concepts/margin-over-servicing.md) story. Tracked in the [thesis ledger](./ledger.md).