---
type: organization
title: Upsun
description: Managed hosting/CDN (Platform.sh) used for AREA 17 projects including NASEM.
tags:
  - client
  - upsun
---
# Upsun

Upsun is the managed hosting and CDN platform (from Platform.sh) used for AREA 17 projects, including the [NASEM Site](/projects/nasem-site.md). It provides fixed-plan environments rather than self-serve scaling.

## Why it matters

Upsun's operational model creates release-process friction. There is no self-serve console for environment or edge configuration: fixed-plan environments and bot-management VCL changes both require support tickets, which introduces lag into the release cadence. This is a recurring drag on the [environment hygiene](/concepts/environment-hygiene.md) and [release engineering](/concepts/release-engineering.md) workflows on NASEM.

Upsun was also the root cause of staging build issues: its configuration YAML did not compile assets the way production did, so staging builds diverged from production behavior.

Because bot management cannot be procured through Upsun and the app is already built for Fastly, the NASEM team decided to pursue Fastly (with bot manager) directly rather than route it through Upsun.

## Key people

- Charles

## Related

- Project: [NASEM Site](/projects/nasem-site.md)
- Concept: [Environment Hygiene: Pre-Prod & QA Workflow](/concepts/environment-hygiene.md)
- Concept: [Bot Management / Edge & SEO Trade-offs](/concepts/bot-management-seo.md)
