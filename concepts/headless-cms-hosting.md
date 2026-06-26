---
type: concept
title: Headless CMS Hosting & Deployment Trade-offs
description: The static-export and hosting constraints created by serving a headless CMS site from a CDN with no public server.
tags:
  - concept
  - theme
---
# Headless CMS Hosting & Deployment Trade-offs

The cluster of architectural constraints that appear when a headless-CMS site must be served as **static files from a CDN with no public-facing server** — a profile most sharply expressed by the [Jane Street](/clients/jane-street/overview.md) engagement.

## The idea

A headless CMS (Payload, in Jane Street's case) needs a running Node server to operate. But Jane Street's security posture requires that nothing public-facing run a server — the site has to ship as static files served from a CDN. Reconciling those two facts forces a specific, awkward pipeline.

## The trade-offs

- **Webhook-driven static export** — CMS changes fire a webhook that rebuilds and re-exports the static site, rather than serving dynamically.
- **No ISR** — incremental static regeneration isn't available; every change means a rebuild.
- **Two parallel Payload instances during development** — the dev/editing instance and the build pipeline run separately.
- **On-prem hosting, SSO, and access constraints** — the site lives behind the client's infrastructure and identity controls, not a typical cloud deploy.

## Why it recurs

It is an out-of-sequence, "liminal" project: the usual build-then-host sequence is inverted by the hosting constraint, so infrastructure decisions have to be made before the UX and foundation are settled — a standing source of risk when conceptual ambition runs ahead of a shippable, functioning site.

## Concrete example

- **[Jane Street Website Redesign](/projects/jane-street-redesign.md)** — the canonical case: Payload behind a static-export pipeline, served from a CDN, with on-prem hosting, SSO, and access restrictions shaping the entire build.
