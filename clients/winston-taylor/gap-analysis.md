---
type: note
title: Gap Analysis
description: Weighted matrix cross-reference audit identifying blockers, miscategorized, and reconciled items for Project Meridian.
tags:
  - client
  - winston-taylor
  - area17
---
# Gap Analysis

*Project Meridian | Weighted Matrix Cross-Reference Audit | February 2026*

We ran the weighted scoring matrix against every discovery document, integration audit, field mapping, and follow-up response to find what's missing, what's underweighted, and what's sitting in the wrong priority bucket. The findings below are organized by urgency, starting with governance blockers that need resolution this week and working down to structural improvements that make the table more useful over time. Items already addressed in the recommendation narrative are at the bottom under Reconciled, they just need corresponding rows added to the table so the commitments are traceable.

# Do Now

These are blockers. They gate other work, they threaten the May 1 date, and they need owners and deadlines attached to them immediately.

## Vendor approval is the gate that gates everything else

TW needs an open-source tech list, WS has "specific questions" they haven't shared yet. The table lists this as blocked, but it's not just another blocked row, it's the one that blocks everything else. The cascading approval approach where dev starts while reviews run in parallel got endorsed by TW, but WS hasn't responded. If vendor approval stalls, May 1 is off the table regardless of how ready everything else is. This needs to be treated as the single highest-priority governance action, and it needs an owner and a deadline attached to it this week.

## Consent philosophy cascades into everything user-facing

TW wants legitimate interest, WS is revisiting opt-in. The table treats this as one row among several consent and privacy items, but it's not a consent banner decision. It's a design-level blocker that gates every form, every analytics tag, every CRM integration, and the entire GTM container configuration. The blast radius is significantly larger than the table conveys, and both privacy teams need to be in a room together soon (my hunch is this is the kind of thing that drifts for weeks if nobody forces the conversation).

## Taxonomy reconciliation is the most cross-cutting dependency in the table

No working session is scheduled. WS has KPMG AI recommendations under review, TW is "heavily invested" in their existing structure. The table lists this as blocked, which is accurate, but doesn't convey that taxonomy gates search, migration, content relationships, and content hubs. It's on the critical path for almost every other Day 1 feature. Getting a working session on the calendar is probably the second-most important action item after vendor approval.

## Redirect strategy determines whether TW lawyers show up in search results

There's no consensus on redirect strategy and it directly affects SEO authority transfer. Given that TW's domain authority can't transfer (the verein retains taylorwessing.com), this isn't just an SEO line item. It determines whether roughly 700 TW lawyer profiles have any organic visibility at launch. The table says blocked, but this should be flagged as a critical-path dependency with real business consequences if it sits unresolved for another few weeks.

## SLA reconciliation blocks the hosting contract

WS wants 99.95% uptime 24/7/365, TW wants 4-hour P1 response during business hours. These are listed as partial but there's no indication of who owns reconciliation or what the deadline is. With Upsun as the hosting partner, these terms need to be finalized before contract signing, and the hosting contract is one of the first things that needs to move. This is blocking on the governance side, not the technical side.

# Fast Follow

These need scoping decisions and architecture calls now, before dev starts. Some are missing from the table entirely, others are miscategorized or underweighted. None of them can wait until after launch to be thought through.

## PE Report has a June 1 deadline, effectively making it a Day 1 decision

The gated content row is listed as partial with a note that gating in Foleon vs CMS is undecided. But the PE Report has a hard June 1 deadline, one month after launch. Given the May 1 constraint, the scoping and architecture decisions around gated content need to happen now, not after launch. The priority in the table should reflect that this is timeline-critical (and probably the first post-launch deliverable that'll actually get tested in production).

## PDF bio generation is marked Required but buried under a Phase 2 feature

The lawyer profile field mapping has pdf_enabled as required. The integrations audit shows WS uses a bio generator built by Rubylaw that lets BD teams export packets of bios into Word. The table captures "document generator" as Phase 2 nice-to-have, but individual PDF bio download and the RFP packet generator are two different features at two different complexity levels. Individual bio PDFs are required and relatively straightforward, the full document generator is Phase 2 and significantly more complex. These should be separated into their own rows with different priorities.

## Dual-CRM routing complexity is greater than two separate integrations

The table covers forms and CRM individually across several rows, but the combined complexity of routing a single contact form submission to both Vuture and Nexl simultaneously, with different field schemas, different authentication, and potentially different consent bases, is an architectural design item. It's not just wiring up two integrations, it's designing a routing layer that handles the fan-out gracefully. This should be called out as a design consideration in the table, because the effort estimate for "CRM integration" understates it when you're actually building one form that talks to two systems with different contracts.

# Do Next

Infrastructure items that need rows in the table and should be built during the MVP sprint. These aren't governance blockers, but they're live dependencies or Day 1 requirements that the table currently doesn't capture.

## Video embed and FTP asset replacement are Day 1 infrastructure with no rows

Two items from the integrations audit that need representation in the table. Vimeo and YouTube are both marked do next, TW listed video embeds as Day 1, and there's a brand video likely at launch, but the table doesn't capture the specific embed infrastructure (oEmbed, responsive players, lazy loading for performance). Separately, Filezilla is marked keep with the note that it's an FTP site hosting videos and documents they don't want indexed by Google. That's a live dependency, those non-indexed assets need to go somewhere in the new stack, and the table should capture where.

## API credential and secrets management

Follow-up question 20 explicitly discusses how API credentials should be managed across two IT organizations, and WS said they'd prefer AREA 17 handle secrets management if fully managed. This is an infrastructure requirement with no row in the table. It's not a hard blocker, but it's the kind of thing that becomes a problem during integration testing if it hasn't been thought through, and it touches the managed hosting relationship with Upsun.

## RSS and podcast infrastructure

WS uses RSS feeds to push to Mondaq and podcast platforms. Mondaq integration is listed as post-launch, which is fine, but RSS feed generation is a CMS-level feature. If WS wants Mondaq integration post-launch, the RSS infrastructure needs to exist from Day 1 or it becomes a retrofit. Separately, both firms have active podcast initiatives and the "Defining Moments" podcast is described as being in the works for both teams. Podcasts as a content type are Phase 2, but basic embed support (Apple Podcasts, Spotify links) for a jointly-branded podcast launching around the same timeframe could collide with MVP. Worth confirming whether this is truly post-launch or if basic embed support needs to be in scope.

# Do Later

These are improvements to the table itself. They don't affect what gets built, but they'd make the table significantly more useful as a project management and governance tool going forward.

## The table needs structural improvements to be a real project management tool

Three things would make the table significantly more useful. First, there's no dependency column, many blocked items block other items (taxonomy gates search, migration, and content hubs; consent philosophy gates forms, analytics, and CRM; redirect strategy gates SEO authority transfer) and the table has no way to express those cascading relationships. Adding a "blocks" column would make the critical path visible.

Second, blocked items don't indicate who needs to act. "Blocked" is a state, not an action. Adding an owner column ("WS Privacy Team," "Joint Governance," "TW/UNRVLD") would make the table actionable for project managers instead of just descriptive.

Third, the qualified column criteria could be tighter. It appears to mean "fully scoped and unblocked" but the application isn't consistent, some partial-status items are marked false even when the gap is minor. Tightening the criteria would make this column actually useful for filtering.

# Reconciled

These items surfaced in the cross-reference audit but are already addressed in the recommendation narrative (Laravel Twill tab, CMS Evaluation tab, or both). The architectural commitments are documented, they just need corresponding rows added to the weighted matrix table so the commitments are traceable and scorable.

## Content hubs are already described as Day 1

The CMS Evaluation tab's AI Readiness section explicitly describes the content hub architecture as a Day 1 feature, with ad-hoc tagging and dynamic aggregation supported natively by the content model. The cross-reference audit flagged this because the table has no row for it, but the feature itself is already scoped and committed in the narrative. Just needs a table row so it's visible in the scoring.

## Structured data and Schema.org markup is already committed

Both recommendation tabs describe server-side rendered pages with structured data, and Appendix B in the Laravel Twill tab frames machine-readability as a Day 1 design constraint based on the Feb 16 discussion. The audit flagged this because the AEO row in the table captures the concept but there's no explicit row for the structured data implementation itself (JSON-LD, Schema.org). Adding a row makes the infrastructure commitment traceable.

## Meilisearch schema design is already documented as Day 1

Both tabs explicitly state "index schema and data model designed for this from Day 1, Phase 2 activates Meilisearch's built-in AI capabilities." The audit flagged this because the table lumps it under the Phase 2 AI/NLP search row without distinguishing between the schema work (Day 1) and the AI-facing search UI (Phase 2). Splitting or annotating the row would make the Day 1 deliverable visible.

## Laravel AI middleware is already described in the evaluation

The CMS Evaluation tab's AI Readiness section says "Laravel's middleware layer routes requests through any AI service with an API." The audit flagged this because the table has no row for the middleware scaffolding, which is distinct from the Phase 2 AI search feature it enables. Adding a row makes it traceable.

## Content model portability is already a stated architectural principle

Both tabs cover this extensively: the Guiding Principles section, the Lock-in and Portability section, and multiple references to "content model defined in code that AREA 17 writes and Winston Taylor owns, PostgreSQL standard schema, data exports cleanly." The audit flagged this because it's a contractual and architectural commitment that should be in the features table, not just in prose. Adding a row makes it scorable and comparable across the three CMS options.

---

Related: [Features & Capabilities Missing](/clients/winston-taylor/features-capabilities-missing.md), [CMS Evaluation](/clients/winston-taylor/cms-evaluation.md), [Laravel Twill Recommendation](/clients/winston-taylor/laravel-twill-recommendation.md).
