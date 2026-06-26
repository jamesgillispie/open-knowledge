---
type: project
title: Winston Taylor MVP (Project Meridian)
description: MVP website for the merged law firm with a full insights/news/events section.
tags:
  - project
  - winston-taylor
---
# Winston Taylor MVP (Project Meridian)

MVP website for the merged law firm [Winston Taylor](/clients/winston-taylor/overview.md). Scope expanded via amendment to support a full insights / news / events section — roughly **1,053 migrated items** across articles, series ("blogs"), podcasts/video, and events.

## Summary

Key workstreams:

- **Content migration** + a legacy-firm disclaimer banner on migrated content
- **Search** via [Meilisearch](/clients/meilisearch/overview.md)
- **Forms** via Formie, routing to dual CRMs
- **Gated content** via [Foleon](/clients/foleon/overview.md) (short-term)
- **OneTrust** CMP
- **Bio / SSO**
- **Redirect strategy** across legacy domains

## Status

Active — MVP build. Functional site targeted by end of May; content and gated reports by June 1.

## Key decisions

- **Information architecture:** rename "blogs" to "series" with a dedicated landing; split into three separate listings (news / insights / events) rather than one filtered listing, since events need date-based sorting.
- **Events + gating:** keep gated content on [Foleon](/clients/foleon/overview.md) for MVP; auto-recategorize/archive past events once a date passes; externalize event registration (Zoom / On24); Vimeo for hosting + YouTube for reach.
- **Visual:** lighter insights/news cards with a stroke hover state and a bright search-results theme; auto-display a legacy-firm disclaimer banner only on migrated content.
- **Forms / consent:** recommend Formie as the unified form platform routing to two CRMs; client must procure the OneTrust CMP themselves, urgently, as it blocks site completion.
- **Search:** stand up [Meilisearch](/clients/meilisearch/overview.md) Cloud (AREA 17 bills client); start small/medium and scale self-serve, reusing AREA 17's existing account.

## People

- [Seti](/people/seti.md)
- [James Gillispie](/people/james-gillispie.md)

## Related

- Org: [Winston Taylor (Project Meridian)](/clients/winston-taylor/overview.md)
- Vendor: [Foleon](/clients/foleon/overview.md)
- Vendor: [Meilisearch](/clients/meilisearch/overview.md)
- Concept: [Content Migration, Taxonomy & CMS Templating](/concepts/content-migration-taxonomy.md)
