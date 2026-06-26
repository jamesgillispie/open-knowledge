---
type: project
title: NASEM Site (Sprint / Care Engagement)
description: Ongoing enhancement of the launched National Academies Twill site via sprint-based releases.
tags:
  - project
  - national-academies
---
# NASEM Site (Sprint / Care Engagement)

Ongoing enhancement and maintenance of the launched [National Academies (NASEM)](/clients/nasem/overview.md) Twill site, run as sprint-based work with large multi-branch releases deployed through [Upsun](/clients/upsun/overview.md).

## Summary

The engagement spans a wide enhancement surface:

- Multi-track opportunities plus past-awardees tabs
- Collection-overlay permalinks
- URL restructuring (coordinated with F5 / ITS)
- Betty AI sitemap integration
- Flagship-events schedule tabs (TRB)
- OpenSearch search advancement (and regression handling)
- PDF-download auth bugs
- BigQuery / GA audit
- Fastly bot mitigation

The **Growth 28.01 "monster release"** (~32-38 branches) was the largest to date, and motivated using [Claude Opus](/clients/anthropic/overview.md) to audit the release branch for regressions before merging.

## Status

Active — post-launch maintenance/enhancement. Roughly **$80k of care budget remaining**, planned as two six-week sprints (Sprint 1 engineering, Sprint 2 strategy/design).

## Key decisions

- **Scope discipline:** new client requests must be filed as separate tickets, not appended to in-flight or in-QA tickets; producers push back on scope creep.
- **Release cutoff:** tickets not client-approved before the Tuesday release roll to the next Opportunity Sprint rather than a future release in the current contract.
- **Budget plan:** convert the remaining ~$80k 2027 care budget into two six-week sprints; client submits a prioritized backlog to estimate.
- **AI regression auditing:** use [Claude Opus](/clients/anthropic/overview.md) to audit the large release branch for regressions before merging.
- **Bot management:** pursue [Fastly](/concepts/bot-management-seo.md) (with bot manager) directly, since the app is already built for Fastly and it can't be procured through [Upsun](/clients/upsun/overview.md).
- **URL restructure:** handle as low-hanging fruit first via a redirect capsule — crawl the URL list and test against F5 redirects to avoid loops.
- **Opportunities listing:** make it a toggleable tab; keep past-awardees and opportunities as separate tabs; show metadata filters only if universal across child programs.
- **Bot/SEO trade-off:** blocking bot traffic via robots.txt query-param blocking fixed server load but blocked ~66K URLs in Search Console, sharply dropping impressions — a trade-off under research (see [Bot Management / Edge & SEO Trade-offs](/concepts/bot-management-seo.md)).

## People

- [Talia](/people/talia.md)
- [Stacy](/people/stacy.md)
- [Mark](/people/mark.md)
- [Nikki (Nicola)](/people/nikki.md)
- [Eric](/people/eric.md)
- [Clara](/people/clara.md)
- [James Gillispie](/people/james-gillispie.md)

## Related

- Org: [National Academies (NASEM)](/clients/nasem/overview.md)
- Vendor: [Upsun](/clients/upsun/overview.md)
- Concept: [Release Engineering: Large Multi-Branch Merges](/concepts/release-engineering.md)
- Concept: [Sprint vs. Retainer Model for Complex Platforms](/concepts/sprint-vs-retainer.md)
- Concept: [Bot Management / Edge & SEO Trade-offs](/concepts/bot-management-seo.md)
