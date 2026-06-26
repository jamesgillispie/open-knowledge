---
type: project
title: FTZ Analytics / GTM Tracking Program
description: AREA 17's click/event tracking offering and the push to make GTM tracking standard practice via a contract-stage permission letter.
tags:
  - project
  - area-17
---
# FTZ Analytics / GTM Tracking Program

[AREA 17](/clients/area-17/overview.md)'s click/event tracking offering and the effort to make it standard practice on every engagement. FTZ implements a clean, resilient GTM pattern — **single event, single tag, multiple triggers, with clearly named AREA 17 events** — and ties campaign activity back to conversions via BigQuery/Looker. It is part of the analytics through-line that runs across AREA 17 engagements ([Analytics as an Engagement Through-Line](/concepts/analytics-through-line.md)).

## Status

Rolling out; aiming for standard practice on all new work. FTZ was demoed a couple of weeks before June 25; [Mark](/people/mark.md) had assumed it was already fully in place.

## Key decision

**Make FTZ analytics / GTM tracking standard practice for every new engagement**, gated by a reusable **boilerplate permission letter** sent at the contract stage. The framing positions tracking as a client benefit — "to improve your X, we'd like permission to implement GTMs for tracking" — securing buy-in early, before anyone is paying close attention. James to draft the template in Confluence (Mike may have started it).

## Implementation considerations

- **Client-owned GTM containers/workspaces** — clients like Nation have their own GTM account, BigQuery, and an in-house analytics team, so publishing rights and access are not always clear. The working assumption is that AREA 17 events can live in a client's primary workspace if clearly labeled, and that multiple workspaces can run simultaneously within one container (needs validation).
- **Event cleanup before deployment** — existing tracked events on a new site may overlap or conflict with FTZ events; audit and delete redundant events before rerunning to avoid duplication.
- **Tied to BigQuery/Looker** for campaign-to-conversion attribution (e.g. campaign performance tied to museum ticket purchases).

## People

- [James Gillispie](/people/james-gillispie.md) — owns the technical pattern and the permission-letter template.
- [Tucker](/people/tucker.md) — analytics/data layer collaborator.

## Organization

[AREA 17](/clients/area-17/overview.md)
