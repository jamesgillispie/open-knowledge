---
type: organization
title: Foleon
description: Interactive/gated content platform used as a Sitecore workaround on Winston Taylor.
tags:
  - client
  - foleon
---
# Foleon

Foleon is an interactive and gated-content platform that the Winston Taylor (Taylor Wessing side) team uses as a workaround for Sitecore's limitations. It is part of the [Winston Taylor MVP (Project Meridian)](/projects/winston-taylor-mvp.md).

## Why it matters

Foleon fills a gap Sitecore cannot: rich, gated, interactive content experiences. But it carries two material concerns:

- **SEO and journey loss** — Foleon content lives on a separate domain, breaking the SEO profile and the on-site user journey.
- **Off-brand styling** — the experience does not fully match the site's brand.

## Decision

Gated content stays on Foleon for the MVP. The long-term goal is to replace it with an in-CMS "super template" that delivers the same gated/interactive capability natively, recovering SEO and brand control.

## Related

- Project: [Winston Taylor MVP (Project Meridian)](/projects/winston-taylor-mvp.md)
- Org: [Winston Taylor (Project Meridian)](/clients/winston-taylor/overview.md)
- Concept: [Content Migration, Taxonomy & CMS Templating](/concepts/content-migration-taxonomy.md)
