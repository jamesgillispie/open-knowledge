---
type: concept
title: Bot Management / Edge & SEO Trade-offs
description: Blocking and rate-limiting AI bots at the edge, and the SEO/server-load trade-offs that come with it.
tags:
  - concept
  - theme
---
# Bot Management / Edge & SEO Trade-offs

Across engagements, a recurring operational priority is controlling the flood of automated traffic hitting client sites. On the [NASEM Site](/projects/nasem-site.md), bot-to-human traffic ratios have run as high as 9:1, driving real server load and cost without serving real users. The work is to block or rate-limit AI crawlers and scrapers at the edge while protecting legitimate search indexing and human visitors.

## Why it recurs

The explosion of AI crawlers (training scrapers, agent fetchers, low-quality bots) has turned bot management from a back-office concern into a front-line infrastructure and cost issue. It sits at the intersection of three competing pressures: server cost, SEO/discoverability, and the platform constraints of whatever hosting the client is on.

## Key tensions and facts

- **Hosting constraints make mitigation slow.** On [Upsun](/clients/upsun/overview.md), VCL (Varnish) changes are ticket-based rather than self-serve, so every edge rule change requires a support round-trip. Fastly's dedicated bot manager could not be procured through Upsun, removing the cleanest off-the-shelf option.
- **Crude blocking has SEO side effects.** A robots.txt query-parameter blocking approach successfully cut server load, but it also tanked impressions in Google Search Console — a direct illustration that aggressive bot mitigation can suppress legitimate indexing if not carefully scoped.
- **Edge vs. CMS redirect strategy.** Where redirects live (at the edge/CDN vs. inside the CMS) is a recurring decision, with implications for performance, maintainability, and bot handling.
- **Redirect-loop avoidance.** F5/ITS-layer redirects must be coordinated to avoid redirect loops, another reason edge configuration is treated carefully.

## Through-line

The pattern is that there is no free lunch: every lever (robots.txt, query-param blocking, edge VCL, a bot manager) trades server cost against SEO visibility and against platform friction. The pragmatic stance is to mitigate at the edge where possible, measure SEO impact in Search Console, and push hosting partners for self-serve edge control rather than ticket-based changes.

Related: [Bot Management / Edge & SEO Trade-offs](/concepts/bot-management-seo.md) connects to [AEO/GEO & AI as a Site Visitor](/concepts/aeo-geo.md) — the flip side of blocking bots is deciding which AI agents you *want* on the site.