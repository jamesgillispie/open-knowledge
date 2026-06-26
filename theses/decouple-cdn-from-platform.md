---
type: thesis
title: Decouple the CDN from the platform
description: As bot traffic dominates, coupling the CDN to the hosting platform (Upsun) is a structural liability; running the edge independently (Fastly/Cloudflare) is the right call.
status: open
confidence: 70
opened: 2026-06-26
horizon: 2026-09-30
tags:
  - thesis
  - infrastructure
  - edge
  - area-17
---
# Coupling the CDN to the hosting platform is now a structural liability

> [!NOTE] Thesis under test
> **Status:** open · **Confidence:** 70% · **Opened:** 2026-06-26 · **Next review:** 2026-09-30

## The bet

**As automated traffic comes to dominate, binding the CDN to the hosting platform (Upsun) costs more than the convenience saves.** Agencies running complex platforms should run the edge independently — Fastly direct or Cloudflare — and within two quarters the decoupled setups will show lower cost and fewer edge incidents than the coupled ones.

## Why I believe it

The traffic mix has flipped and the platform can't keep up with it:

- On Nascent, **~80% of traffic is bots, driving ~$7k/month in preventable overages** ([Weekly Recap, Jun 15–19](/notes/weekly/2026-06-20-recap.md)). On the [NASEM Site](/projects/nasem-site.md), bot-to-human ratios have run as high as **9:1** ([Bot Management / Edge & SEO Trade-offs](/concepts/bot-management-seo.md)).
- The platform makes mitigation *slow and incomplete*: on [Upsun](/clients/upsun/overview.md), VCL/Varnish changes are **ticket-based, not self-serve**, and **Fastly's dedicated bot manager couldn't be procured through Upsun at all** — removing the cleanest off-the-shelf fix ([Bot Management](/concepts/bot-management-seo.md)).
- The decision has already started converging in the field: **both Nascent and NASAM are moving to decouple the CDN from Upsun** (Fastly direct or Cloudflare) for bot management ([Weekly Recap, Jun 15–19](/notes/weekly/2026-06-20-recap.md)).

## What would change my mind

- The decoupled setups *don't* reduce cost or edge-incident rate versus Upsun within two quarters — the overruns were a config problem, not a coupling problem.
- Upsun ships self-serve edge control + a procurable bot manager that closes the gap, making the convenience worth keeping.
- Decoupling introduces enough operational drag (two vendors, redirect-loop risk across the F5/ITS layer) that net total cost of ownership rises.

## Scorecard

- **2026-06-26** — Opened at 70%. The direction is already in motion on two projects, so the *decision* is largely made; what's genuinely under test is whether the **economics and incident rate actually improve** once the migrations land. Post-Tuesday bot-blocking work is the first data point.

## What this feeds

The NASAM and Nascent infrastructure decisions, the v2 Technical Director Guide's edge-strategy section, and the cost-of-bots argument that connects [bot management](/concepts/bot-management-seo.md) to [AEO/GEO](/concepts/aeo-geo.md) — which automated visitors you block vs. welcome. Tracked in the [thesis ledger](./ledger.md).