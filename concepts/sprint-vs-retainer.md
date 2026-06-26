---
type: concept
title: Sprint vs. Retainer Model for Complex Platforms
description: Why short sprints push hard problems to the last moment, and the case for retainer/lead-dev models.
tags:
  - concept
  - theme
---
# Sprint vs. Retainer Model for Complex Platforms

A recurring engagement-model tension: short, time-boxed sprints tend to push the genuinely hard problems — API synchronization, search, integrations — to the very last moment, where they compound regressions, code churn, and QA load right when there is the least slack to absorb them.

## The problem

Sprints front-load the visible, well-understood work and back-load the risky, interdependent work. By the time the hard systems-level problems surface, the sprint is nearly over, so fixes land late, get rushed, and trigger regressions elsewhere. The [NASEM Site](/projects/nasem-site.md) is the clearest example: a complex platform whose hardest pieces kept arriving at the end of sprint windows.

## The emerging consensus

Complex platforms like [National Academies](/clients/nasem/overview.md) are better served by a full-time retainer or dedicated lead-developer model than by discrete sprint engagements. A retainer gives continuity over the hard, slow-burning problems (API sync, search relevance, environment stability) and lets the team sequence risk deliberately instead of being forced into a sprint cadence that doesn't match the work.

## Why it recurs

The sprint model is attractive commercially and easy to scope, but it assumes work decomposes cleanly into independent increments. Platforms with deep integration surfaces violate that assumption, so the same late-stage crunch reappears project after project.

## Through-line

Match the engagement model to the shape of the work: independent, well-bounded scopes can sprint; deeply interdependent platforms need a retainer/lead-dev model that prioritizes continuity over cadence. This connects to [Release Engineering: Large Multi-Branch Merges](/concepts/release-engineering.md) and [Environment Hygiene: Pre-Prod & QA Workflow](/concepts/environment-hygiene.md), both of which are downstream symptoms of a cadence that doesn't fit the platform.