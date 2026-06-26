---
type: concept
title: Search Platform Evaluation & Relevance
description: Recurring evaluation and tuning of search platforms and relevance ranking across AREA 17 engagements.
tags:
  - concept
  - theme
---
# Search Platform Evaluation & Relevance

A recurring strand of work across AREA 17 engagements: choosing a search platform, then keeping its **relevance** correct as the site evolves. The two poles are platform selection (which engine, on what pricing/hosting model) and relevance tuning (keyword weighting, faceting, and guarding against ranking regressions).

## The idea

Search is never "done" at launch. It is a configurable system — keyword weighting, title/exact-match ranking, acronym handling, faceting — that drifts as config files and content change. Treating search as MVP-then-iterate makes relevance regressions a standing risk that needs explicit guardrails.

## Concrete examples

- **[Winston Taylor MVP](/projects/winston-taylor-mvp.md)** — selected **Meilisearch** (self-hosted, evaluated against Algolia/OpenSearch) for the composable architecture, with backend keyword weighting and faceting and document-based pricing. The index schema and data model were designed from day one so that Phase 2 could activate Meilisearch's built-in AI/natural-language search.
- **[NASEM Site](/projects/nasem-site.md)** — an **OpenSearch** MVP that surfaced relevance regressions after launch: an acronym keyword was dropped from a config file (staging-only, but high-impact for an acronym-heavy org), and relevancy/title-match ranking regressed on both staging and production after being previously fixed and verified. James trained [Mark](/people/mark.md) on OpenSearch and configurations post-launch.

## The proposed guardrail

[Nikki](/people/nikki.md) proposed a **hierarchical regression test suite** for search — acronym matching always first, then title/exact match, then secondary relevancy — run before any search-related deploy to staging or prod. James separately proposed a **pre-production environment** to reduce staging noise and catch regressions earlier (see [Environment Hygiene](/concepts/environment-hygiene.md)). Together these aim to make relevance regressions catchable before they reach users.
