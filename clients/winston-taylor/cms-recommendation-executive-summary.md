---
type: concept
title: CMS Recommendation — Tab 1 Executive Summary
description: Project Meridian executive summary recommending Twill on Laravel as the Winston Taylor CMS.
tags:
  - client
  - winston-taylor
  - area17
---
# CMS Recommendation: Twill on Laravel

*Project Meridian | AREA 17 Technical Direction | February 2026*

---

## Context

We completed discovery with both firms, gathered requirements, audited the existing platforms, and mapped the integration landscape. We evaluated three CMS platforms against this project's specific requirements, timeline, and operating model. What follows is the recommendation.

Hard deadline: **May 1** (merger announcement / verein separation).

---

## Guiding Principles

Before getting into platform specifics, these are the technology principles that shaped the evaluation. They come directly from what both firms described in discovery.

**Open source over proprietary** — Technology that's publicly available, community-maintained, and free from vendor licensing constraints. No multi-year contracts, no auto-renewals, no proprietary content schemas.

**Composable over monolithic** — The CMS handles content. Search, media delivery, CRM routing, and analytics connect through dedicated services that can be swapped, upgraded, or replaced independently. The architecture grows with the firm rather than constraining it.

**No vendor lock-in** — Content model defined in code you own. Data in PostgreSQL with standard schemas. Technology that's transferable if circumstances change.

**Universal development** — The brief was explicit: the tech stack should be widely adopted, with a large talent pool and transferable skills. No niche platforms, no proprietary frameworks.

**Agency-managed operations** — Both IT teams described a preference for one relationship, one team accountable for hosting, deployment, infrastructure, and ongoing support. Not a vendor-managed DXP with another relationship to manage.

Everything that follows is measured against these principles.

---

## The Recommendation

**We recommend Twill on Laravel as the CMS for the Winston Taylor website.**

Twill is open source, composable, and built on one of the most widely adopted frameworks in PHP. It's maintained by A17, and it's the strongest fit against this project's requirements, timeline, and operating model. We're making this recommendation with confidence.

A17 has delivered Twill at this scale for organizations with comparable content complexity, including the International Energy Agency, Open Society Foundations, the Guggenheim, and the National Academies. We've also prepared a tailored CMS demo based on Week 1 build work, which we can walk through live to show how the editorial experience maps to the requirements both teams described.

---

## What Both Firms Asked For

The brief and discovery sessions were consistent across both sides:

- Editorial control and self-service CMS capabilities
- Flexible templates with modular content blocks
- Integration with existing systems (Vuture/OnePlace for TW, Nexl/Foundation for WS)
- Multilingual support
- AI search and personalization post-launch
- AEO readiness for the MVP
- Security and governance across two IT teams
- Robust media handling with bulk operations
- Content tagging and taxonomy
- WCAG AA accessibility
- Universal development, not niche

---

## Why Twill

**Editorial control** — Block editor gives both teams flexible, modular templating. Role-based access control and editorial approval workflows handle governance across two teams natively.

**Structured content modeling** — Professional directories, capability pages, multilingual content with regional variations, high-volume publication workflows. These are the use cases Twill was designed for.

**Media handling** — Bulk operations, responsive cropping, and image optimization are native to the platform.

**Integration-ready** — Composable architecture connects to each firm's existing systems through dedicated service layers, not through a monolithic DXP.

**Multilingual** — Built in, with regional variant handling.

**No procurement cycle** — Open source (Apache 2.0, on MIT-licensed Laravel). No license negotiation, no contract to finalize. Dev environment goes up the day the stack is approved.

**Universal development** — Laravel has one of the largest developer ecosystems in PHP. The codebase is public on GitHub. LLMs are trained extensively on Laravel's open documentation and codebase, which directly accelerates development productivity in ways that closed-source DXPs simply can't benefit from. The brief asked for development that's universal, not niche. That's what this is.

---

## Why Not the Alternatives

We evaluated two other platforms seriously. Neither is a bad platform. The gaps are specific to this project.

**Optimizely** — Procurement cycle runs 4-8 weeks minimum, which is incompatible with May 1. Pricing starts at ~$36K/year and scales well above $200K at this content volume, on multi-year auto-renewing contracts with proprietary content schemas. Both IT teams described a preference for agency-managed over vendor-managed. Timeline and contract structure don't fit.

**Payload CMS** — A17 has real production experience with Payload and is actively building on it for another client. Payload is strong as a rapid CRUD builder for Next.js projects, but it's not yet a mature CMS at the level this project requires. The editorial workflows both teams described need more custom frontend development in Payload than in a platform where those workflows are built in. The content model is deeply relational (thousands of profiles cross-referenced with capabilities, offices, sectors, insights, multilingual variants), and PostgreSQL handles that more naturally than Payload's MongoDB default, even with the PostgreSQL adapter now available. Figma's recent acquisition of Payload also introduces uncertainty about the platform's long-term strategic direction. A17 pushed Payload to its limits on ElevenLabs (a simpler site than this project), which reinforced that Twill is the better fit for this content complexity. Our deepest institutional knowledge, production tooling, and design system (Vitrine) live in the Twill/Laravel ecosystem.

*Full comparative evaluation in [Tab 2: Deep Evaluation](/clients/winston-taylor/cms-recommendation-deep-evaluation.md).*

---

## Architecture: Day 1 and Beyond

The architecture is composable. The CMS handles content modeling and editorial workflows. Everything else connects through dedicated services that A17 builds and the firm owns.

### MVP (Day 1)

| Layer | Solution |
|---|---|
| CMS | Twill on Laravel |
| Search | Meilisearch (self-hosted, includes AI capabilities, no SaaS procurement) |
| Media | Twill native media library + image optimization via Cloudflare |
| Forms | Centralized handling, routed to each firm's CRM via Laravel queue |
| Hosting | Upsun Dedicated (contract through A17) |
| CDN / Security | Cloudflare (already in use by both firms) |
| Accessibility | Siteimprove (already in use) |

### Phase 2 (Post-Launch)

- **Algolia** — When the firm is ready to offload search hosting and add search analytics, the data model and index schema are designed for this from Day 1. Migration from Meilisearch is a driver swap, not a rearchitecture. (Both Meilisearch and Algolia support AI-powered search; the move to Algolia is about managed hosting and analytics, not gaining AI capabilities. Meilisearch Cloud is also an option as an intermediate step.)
- **DAM integration** — Media library is abstracted so a platform like Bynder plugs in by changing where the service points.
- **Deeper CRM integration** — Potentially consolidated across firms.
- **Multilingual expansion** — WS would prioritize Spanish and Portuguese.
- **Content personalization and experimentation**
- **Content syndication and distribution automation**

Each new capability goes through its own procurement at the point of adoption, not before launch. None require changing the CMS or renegotiating a vendor contract.

---

## AI and AEO Readiness

Both firms raised this in discovery. WS wants to prioritize answer engine optimization over traditional SEO. TW described AI-enhanced search and personalization as near-term goals.

- Server-side rendered pages with structured data are exactly what AI agents need to consume, no client-side JavaScript assembly required for content to be indexable.
- Laravel's middleware layer can route requests through any AI service with an API.
- Content hub pages (AI regulation, COVID response, Crown Act, emerging topics) are a **Day 1 architecture feature**, not a Phase 2 request. The content model supports ad-hoc tagging and dynamic aggregation natively.

---

## No Lock-In

- Content model is defined in code that A17 writes and the firm owns.
- Data lives in PostgreSQL with a standard schema.
- Built on Laravel, widely adopted, fully transferable.
- Data exports cleanly. Content model is documented. Frontend is standard web technology.
- A17 will continue as the technology partner. But the architecture doesn't require it. That's a principle we build around.

---

## Operating Model and Hosting

The operating model both firms described, A17 owns hosting, manages the deployment pipeline, handles infrastructure, continues under maintenance retainer, is exactly how we deliver Twill projects. This is a white-glove engagement: one relationship, one team, accountable for the whole stack.

Hosting runs on Upsun Dedicated and Cloudflare, both proven platforms with established security compliance and enterprise track records. The hosting contract passes through A17, so there's no separate vendor relationship to manage.

- No procurement blockers.
- Dev environment stands up immediately on stack approval.
- Ships by May 1.

---

## Recommendation

Twill is the clearest fit against this project's requirements, timeline, and operating model. It ships by May 1, the composable architecture grows with the firm rather than constraining it, there's no lock-in or multi-year contract, and it's maintained by the same team that will build, host, and support the site.

That's the recommendation.

---

## Appendix A: Discovery Themes That Shaped the Evaluation

These topics came up repeatedly in discovery and directly influenced the stack recommendation. They aren't guiding principles in the same sense as the ones above, but they're worth documenting because they were consistent across both firms and both IT teams.

### Content Hubs

Both firms described a need to quickly stand up topic-based pages that pull together lawyers, insights, case studies, and events around emerging issues. AI regulation, COVID response, and the Crown Act were the examples used in discovery. The ask was for editorial teams to create these aggregations on their own using ad-hoc tags outside the formal taxonomy, without filing a dev ticket every time a new issue surfaces. Twill's block editor and content tagging handle this natively. The structured data schema reflects those groupings dynamically, so answer engines pick up the new aggregation without additional technical work. This is a Day 1 architecture feature, not a Phase 2 request.

### Security and Governance

SOC 2 compliance came up in the Feb 25 session as a hard requirement, and SSO integration with Azure AD/MFA was discussed alongside it. The security questionnaire process is already initiated. Both IT teams need to vet the stack, and this was a consistent theme across multiple meetings that directly shaped our evaluation criteria. The stack was chosen with this in mind. Upsun and Cloudflare are both proven, security-compliant platforms that give both IT teams something concrete to align around.

### AI and AEO Readiness

Both firms raised this in discovery, not as a Phase 2 nice-to-have but as a design constraint from Day 1. WS wants to prioritize AEO over traditional SEO. TW described AI-enhanced search as near-term. The Feb 16 meeting had extended discussion about structuring the content model to be machine-readable from launch. This is baked into how we're thinking about the content architecture, not bolted on later.

### No Throwaway Work

The Feb 16 session had the explicit framing: "we don't want to build something and then just throw it out and start over." This shaped the composable architecture argument and is worth calling out on its own. Every decision in this stack is designed to carry forward. Nothing here is scaffolding that gets torn down in a future phase.
