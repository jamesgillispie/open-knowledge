---
type: note
title: Features & Capabilities Missing
description: Requirements and commitments missing from, underweighted in, or miscategorized in the features matrix.
tags:
  - client
  - winston-taylor
  - area17
---
# Features & Capabilities Missing

## 🔴 Missing Entirely from the Table

These are requirements or commitments that surface clearly in your discovery materials or the context you provided, but have no corresponding row in the features table:

### 1. Content Hubs / Dynamic Aggregation Pages

You described this as "native from Day 1" — editorial teams using Twill's block builder to create dynamic aggregation pages pulled via ad-hoc tags outside formal taxonomy. This is a distinct content architecture feature, not captured by any existing row. It's different from tagging (row 9) and different from search. It needs its own line because it drives schema design and block builder configuration.

### 2. Structured Data / Schema.org for AEO

Row 58 captures AEO as a concept, but there's no explicit requirement for **structured data markup** (JSON-LD, Schema.org). The integrations audit shows WS currently has Schema.org structured data (marked "Remove" because it's baked into Rubylaw). Your context says "server-side rendered pages with structured data" and "content model structured to be machine-readable from launch." This is a technical implementation requirement that should be its own row — it's foundational infrastructure, not just an SEO nice-to-have.

### 3. Filezilla / FTP Asset Hosting Replacement

The integrations audit shows Filezilla is marked **Keep (Do Now)** with the note: "FTP site that hosts videos and documents that we do not want indexed by Google." This is a live dependency with no corresponding feature row. These non-indexed assets need to go somewhere in the new stack.

### 4. PDF Bio Generation

The lawyer profile field mapping has `pdf_enabled` as **Required**. The integrations audit shows WS uses a "bio generator built by Rubylaw that allows BD teams to export packets of bios into Word." Row 78 captures "Document generator" as **Phase 2 / Nice-to-have**, but individual PDF bio download is marked Required in the field mapping and is a separate, simpler feature than RFP packet generation. These should be separated.

### 5. Vimeo / YouTube Video Embed Infrastructure

Both are marked **Do Next** in the integrations audit. TW listed video embeds as Day 1 (row 16), but the table doesn't capture the specific embed infrastructure (oEmbed, responsive players, lazy loading for performance). With a brand video likely at launch, this is Day 1 infrastructure.

### 6. RSS Feed Output for Content Syndication

WS uses RSS feeds to push to Mondaq and podcast platforms. The Mondaq integration is listed as post-launch (row 92), but RSS feed generation is a CMS-level feature that should be its own row. If WS wants Mondaq integration post-launch, the RSS infrastructure needs to exist from Day 1 or it becomes a retrofit.

### 7. API Credential / Secrets Management

Follow-up question #20 explicitly discusses how API credentials should be managed across two IT organizations. WS said they'd prefer A17 handle secrets management if fully managed. This is an infrastructure requirement with no row in the table.

### 8. Podcast / Audio Embed Support

Both firms have active podcast initiatives. The "Defining Moments" podcast is explicitly described as being "in the works for both teams that will be integrated into the new site." Podcasts as a content type are listed Phase 2 (row 82), but basic embed support (Apple Podcasts, Spotify links) for a jointly-branded podcast launching around the same timeframe seems like it could collide with MVP.

### 9. Content Model Portability / Code Ownership

You emphasized this explicitly: "Content model defined in code, AREA 17 writes it, Winston Taylor owns it. PostgreSQL standard schema, data exports cleanly." This is a contractual/architectural principle that should be documented as a requirement — it's one of the core reasons for the Twill recommendation and should be traceable in the features table.

### 10. Laravel Middleware for AI Service Routing

You described "Laravel middleware routes requests through any AI service" as a Day 1 design constraint. This is distinct from AI/NLP search (Phase 2, row 86). The middleware layer is architectural scaffolding that should exist from launch even if the AI services plug in later.

---

## 🟡 Present but Underweighted or Miscategorized

### 11. Meilisearch Architecture for AI (rows 85-86)

AI/NLP search is listed Phase 2, which is fine for the user-facing feature. But you stated "Meilisearch AI integration (schema designed for it from Day 1)." The table doesn't distinguish between the **schema/data architecture** (Day 1) and the **AI-facing search UI** (Phase 2). The schema design that enables Phase 2 AI search needs to be a Day 1 deliverable or it becomes a refactor.

### 12. Gated Content / PE Report (row 42)

Listed as "Partial" with the note that gating in Foleon vs CMS is undecided. But the PE Report has a **June 1 hard deadline** — one month after launch. Given the May 1 constraint, this is effectively a Day 1 decision. The priority should reflect that this is timeline-critical, not just "Partial."

### 13. Consent Philosophy Alignment (row 54)

Listed as "Blocked" — which is correct — but this is underweighted relative to its blast radius. TW wants legitimate interest; WS is revisiting opt-in. This doesn't just affect a consent banner; it gates **every form, every analytics tag, every CRM integration**. The table treats it as one row among many Consent & Privacy items, but it's a design-level blocker that cascades into Forms, Analytics, CRM routing, and even the GTM container configuration. It needs escalation framing.

### 14. Redirect Strategy (row 52)

Listed as "Blocked" — also correct — but this is described in your context as having "no consensus" and "directly affects SEO authority transfer." Given that TW's domain authority **cannot transfer** (verein retains taylorwessing.com), this isn't just an SEO line item. It determines whether ~700 TW lawyer profiles have any organic visibility at launch. This should be flagged as a critical-path dependency, not just a blocked SEO task.

### 15. SLA Reconciliation (rows 31-32)

The uptime SLA gap (WS wants 99.95% 24/7/365; TW wants 4hr P1 business hours) and P1 incident response gap are listed as "Partial" but there's no indication of who owns reconciliation or what the deadline is. With Upsun as the hosting partner, these SLA terms need to be finalized before contract signing. They should be flagged as blocking the hosting contract.

### 16. Taxonomy Reconciliation (row 48)

Listed as "Blocked" with a note that no working session is scheduled. But taxonomy gates **search, migration, content relationships, and content hubs**. It's the single most cross-cutting dependency in the table. WS has KPMG AI recommendations under review, TW is "heavily invested." The priority/status framing doesn't convey that this is on the critical path for almost every other Day 1 feature.

### 17. Vendor Approval Process (row 72)

TW needs an open-source tech list; WS has "specific questions" not yet shared. This is listed as "Blocked" but it's actually the **meta-blocker** — if vendor approval stalls, nothing else matters. The cascading approval approach (row 73) where dev starts while reviews run in parallel is endorsed by TW but WS hasn't responded. This needs to be called out as the single highest-priority governance action.

---

## 🔵 Structural Observations

### 18. No "Critical Path" or "Dependency" Column

Many blocked items block other items (taxonomy → search + migration + content hubs; consent philosophy → forms + analytics + CRM; redirect strategy → SEO authority). The table has Priority and Status but no way to express **cascading dependencies**. Adding a "Blocks" or "Dependency" column would make the critical path visible.

### 19. No "Owner" Column for Blocked Items

Blocked items don't indicate who needs to act. "Blocked" is a state, not an action. Adding "Action Owner" (e.g., "WS Privacy Team," "Joint Governance," "TW/UNRVLD") would make the table actionable for the project managers.

### 20. "Qualified" Column Semantics

The "Qualified" column appears to mean "fully scoped and unblocked" (true) vs. "has open questions" (false). But Partial-status items are all marked false, even when the gap is minor (e.g., staging environment, row 34, is Confirmed/true despite WS being the only one who requested it). The criteria for Qualified=true vs false could be tighter.

### 21. Dual-CRM Fan-Out Complexity Understated

Rows 37-44 cover forms and CRM individually, but the **combined complexity** of routing a single contact form submission to both Vuture (TW) and Nexl (WS) simultaneously — with different field schemas, different authentication, and potentially different consent bases — is greater than the sum of the parts. This integration pattern should be called out as an architectural design item, not just two separate integration rows.

---

## Summary: Highest-Priority Actions

If I had to rank the top 5 things to address immediately:

1. **Vendor approval process** (row 72-73) — the meta-blocker. Get WS's specific questions and greenlight parallel dev.
2. **Consent philosophy alignment** (row 54) — cascades into everything. Force the joint privacy team discussion.
3. **Taxonomy reconciliation** (row 48) — gates search, migration, content hubs. Schedule the working session.
4. **Redirect strategy** (row 52) — determines whether TW lawyers have organic visibility at launch.
5. **Add the missing rows** — structured data/Schema.org, content hubs, FTP asset replacement, PDF bio generation, content model ownership, and AI middleware scaffolding.

---

Related: [Gap Analysis](/clients/winston-taylor/gap-analysis.md).
