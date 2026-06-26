---
type: project
title: Jane Street Website Redesign
description: Website redesign with a data-driven generative identity, Payload CMS + Next.js.
tags:
  - project
  - jane-street
---
# Jane Street Website Redesign

Website redesign for [Jane Street](/clients/jane-street/overview.md) built around a data-driven, [generative visual identity](/concepts/generative-design-systems.md) — Wolfram-rules / cellular-automata "emergence-convergence" patterns with cursor-trail unmasking.

## Summary

The UX centers on two prompt systems: **contextual prompts** (tooltip-style) and **research prompts** (bottom-of-page routing), driven by a hybrid dynamic/manual CMS controller with a phased rollout (manual to interstitials to AI-driven).

**Stack:** [Payload CMS](/clients/payload/overview.md) + Next.js. The client wants the final site delivered as static files on a CDN with the CMS hosted internally — which collides with Payload's serverful model (see [Headless CMS Hosting & Deployment Trade-offs](/concepts/headless-cms-hosting.md)).

Jane Street is also a candidate for AI personalization (first-party LinkedIn data + site content), one of the use cases driving the [Pinecone Nexus Evaluation](/projects/pinecone-nexus-eval.md).

## Status

Active — design-direction / SteerCo prototype phase. CMS build supported through an October 2026 launch.

## Key decisions

- **Generative direction:** proceed with the Wolfram-rules / cellular-automata pattern direction (Direction 2) as the lead identity, with cursor-trail unmasking; keep Direction 1's controller; cut Direction 3.
- **Prompts:** ship both contextual AND research prompts (not either/or); build as hybrid dynamic with manual CMS override; phase rollout manual to interstitials (~6 months) to AI-driven.
- **Hosting:** present hosting/deployment as trade-off options (static-files-to-CDN with serverful CMS via webhook rebuild, vs. conventional Next.js server) and put the decision back to the client; no ISR without a server.
- **TD handoff:** lean toward [Patrick](/people/patrick-a17.md) taking over Jane Street technical direction so James focuses on [Winston Taylor](/projects/winston-taylor-mvp.md) + BD, driven by James being overloaded across workstreams (see [Director Overload](/concepts/director-overload.md)).

## People

- [Molly](/people/molly.md)
- [Miguel (Mozzie)](/people/miguel.md)
- [Britton](/people/britton.md)
- [Patrick (AREA 17)](/people/patrick-a17.md)
- [James Gillispie](/people/james-gillispie.md)

## Related

- Org: [Jane Street](/clients/jane-street/overview.md)
- Vendor: [Payload](/clients/payload/overview.md)
- Concept: [Generative / Data-Driven Design Systems](/concepts/generative-design-systems.md)
- Concept: [Headless CMS Hosting & Deployment Trade-offs](/concepts/headless-cms-hosting.md)
