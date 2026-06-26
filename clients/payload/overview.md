---
type: organization
title: Payload
description: Next.js-native headless CMS selected for the Jane Street website redesign.
tags:
  - client
  - payload
---
# Payload

Payload is a Next.js-native, Node-server headless CMS selected as the content platform for the [Jane Street Website Redesign](/projects/jane-street-redesign.md). It runs as a serverful Node application rather than a build-time static generator, which puts it at the center of the project's hosting and deployment debate.

## Why it matters

Payload was chosen for its tight Next.js integration and developer experience. AREA 17 is running it under an enterprise key, using features including SSO/OAuth and redirect management. Because Payload is a server-resident CMS, it conflicts with the Jane Street client's stated preference to ship the final site as static files on a CDN with the CMS hosted internally.

## Central tension

The Payload choice frames the [headless CMS hosting trade-off](/concepts/headless-cms-hosting.md) on Jane Street: static-export-to-CDN (CMS triggers webhook rebuilds) vs. a conventional always-on Next.js server. A pure static export forfeits ISR, which requires a running server. The team has chosen to present these as trade-off options and put the decision back to the client.

## Related

- Project: [Jane Street Website Redesign](/projects/jane-street-redesign.md)
- Concept: [Headless CMS Hosting & Deployment Trade-offs](/concepts/headless-cms-hosting.md)
