---
type: concept
title: CMS Recommendation — Tab 2 Deep Evaluation
description: Comparative CMS analysis and supporting rationale for Project Meridian; reference for the executive summary.
tags:
  - client
  - winston-taylor
  - area17
---
# CMS Evaluation: Comparative Analysis and Supporting Rationale

*Project Meridian | AREA 17 | February 2026*
*Reference document — supports the [Executive Summary (Tab 1)](/clients/winston-taylor/cms-recommendation-executive-summary.md)*

---

## Project Requirements

The requirements gathered across discovery with both firms were consistent. These are what all three platforms were evaluated against:

1. **Editorial control and self-service CMS capabilities** — Both teams need to publish and manage content without developer involvement for routine operations.
2. **Flexible templates with modular content blocks** — Page composition should be block-based, allowing editors to assemble pages from a library of reusable components.
3. **Integration with existing systems** — Vuture and OnePlace for TW; Nexl and Foundation for WS. The CMS must connect to these without replacing them.
4. **Multilingual support** — Required at MVP with expansion planned (WS: Spanish, Portuguese).
5. **AI search and personalization** — Post-launch priority for both firms. WS specifically prioritized answer engine optimization over traditional SEO.
6. **AEO readiness for the MVP** — The content architecture and rendering model must support AI agent consumption from Day 1.
7. **Security and governance across two IT teams** — Role-based access control, editorial approval workflows, and a security posture that both IT organizations can sign off on.
8. **Robust media handling with bulk operations** — High-volume image and document management with responsive cropping, optimization, and batch capabilities.
9. **Content tagging and taxonomy** — Deeply relational content model: thousands of professional profiles cross-referenced with capabilities, offices, sectors, insights, and multilingual variants.
10. **WCAG AA accessibility** — Non-negotiable.
11. **Universal development, not niche** — The brief was explicit: the technology stack should be widely adopted, with a large talent pool and transferable skills.

Additional constraint: **May 1 hard deadline** tied to the merger announcement and verein separation. This is not a soft target.

---

## Platforms Evaluated

Three platforms, each representing a different architectural approach:

| Platform | Type | License | Primary Stack |
|---|---|---|---|
| **Twill on Laravel** | Open source, composable CMS | Apache 2.0 (Twill) / MIT (Laravel) | PHP / Laravel / PostgreSQL |
| **Optimizely** | Enterprise DXP (SaaS) | Proprietary | .NET / Proprietary |
| **Payload CMS** | Headless CMS (open source) | MIT | Next.js / TypeScript / PostgreSQL (via adapter) or MongoDB |

---

## Optimizely: Full Assessment

### What it does well

Optimizely is a strong enterprise digital experience platform. It offers bundled capabilities across content management, experimentation, and personalization. The editorial tooling is solid out of the box. It came up in the brief as a platform of interest, and we evaluated it accordingly.

### Where it falls short for this project

**Procurement timeline** — Optimizely's procurement cycle runs 4–8 weeks minimum once you factor in license negotiation, contract review, and certified partner coordination. The May 1 deadline does not accommodate this process. This alone is disqualifying against the current timeline.

**Cost structure** — Pricing starts around $36K annually and scales well above $200K for a deployment at this content scale. Contracts are multi-year and auto-renewing. For a project where both firms described a preference for flexibility and avoiding long-term vendor dependency, this contract structure introduces exactly the kind of constraints they want to avoid.

**Proprietary content schemas** — Content is modeled within Optimizely's proprietary system. The integration model assumes deepening investment in the Optimizely ecosystem over time. Data portability and architectural independence are constrained by design.

**Operating model mismatch** — Both IT teams described a preference for an agency-managed operating model rather than a vendor-managed DXP. Optimizely's delivery model assumes vendor involvement at the platform layer, which adds a relationship and a dependency that neither firm requested.

### Summary

It's not that Optimizely can't do the work. It's that the path to getting started is incompatible with May 1, and the contract structure introduces dependencies that run counter to what both firms described in discovery.

---

## Payload CMS: Full Assessment

### What it does well

Payload is a modern headless CMS originally built on Next.js and MongoDB (now with a PostgreSQL adapter available). It's open source, the developer experience is strong, and it's been gaining real traction in the CMS space. A17 has genuine production experience with Payload — we're actively building on it for another client. This is not a platform we're dismissing; it's one we know well and are investing in.

### Where it falls short for this project

**Platform maturity** — Payload is strong as a rapid CRUD builder for Next.js projects, but it's not yet a mature CMS at the level this project requires. The editorial workflows both teams described (flexible templates, modular blocks, self-service content management, media library with bulk operations) require significantly more custom frontend development than a platform where those workflows are built in. The editorial overhead is higher for this specific set of requirements.

**Database fit** — The content model for this project is deeply relational. Thousands of professional profiles cross-referenced with capabilities, offices, sectors, insights, and multilingual variants. While Payload now offers a PostgreSQL adapter, the platform was architected around MongoDB and PostgreSQL support is still maturing. PostgreSQL handles this kind of structured, taxonomy-heavy data more naturally than Payload's default data layer. This is a data architecture question, not a platform quality question.

**Strategic uncertainty** — Figma's recent acquisition of Payload introduces questions about the platform's long-term direction and governance. For a project that will be in active use for years, platform stability and predictable governance matter.

**Production experience at scale** — A17 pushed Payload to its limits on the ElevenLabs project, which was a simpler site than what this project requires. That experience reinforced that Payload's strengths are in headless-first, developer-driven projects rather than the editorial-heavy, taxonomy-driven content architecture both firms described.

**Institutional depth** — While A17 can deliver on Payload, our deepest institutional knowledge, our production tooling, our design system (Vitrine), and the largest body of shipped work at this scale all live in the Twill/Laravel ecosystem. For a project with this timeline and content complexity, that depth matters.

### Summary

Payload is a strong platform with a growing ecosystem, and A17 continues to invest in it for projects where headless-first architecture is the right fit. For this project's specific content architecture, editorial requirements, and the operating model both firms want, Twill is a better match.

---

## 5. Twill on Laravel: Full Assessment

### Core strength

Twill's core strength is exactly what this project demands: structured content modeling for editorial-heavy, taxonomy-driven sites. Professional directories, capability pages, multilingual content with regional variations, high-volume publication workflows — these are the use cases Twill was designed for.

### Requirement-by-requirement fit

**Editorial control and self-service CMS** — The block editor gives editorial teams the flexible, modular templating the brief described. Content management is self-service by design. Editors compose pages from a library of reusable blocks without developer involvement for routine publishing.

**Media handling** — The media library supports bulk operations, responsive cropping, and image optimization natively. No additional service required at MVP.

**Governance** — Role-based access control and editorial approval workflows handle the requirements across two teams. Permissions are granular and configurable per editorial role.

**Content modeling** — PostgreSQL with a relational schema purpose-built for the kind of taxonomy-heavy, cross-referenced content this project requires. Profiles, capabilities, offices, sectors, insights, multilingual variants — all modeled relationally.

**Multilingual** — Native support with regional variant handling.

**No procurement cycle** — Open source (Apache 2.0 on MIT-licensed Laravel). No license to negotiate, no contract to finalize before work begins. The dev environment goes up the day the stack is approved.

**Universal development** — Laravel has one of the largest developer ecosystems in PHP. Twill's codebase is public on GitHub. LLMs are trained extensively on Laravel's open documentation and codebase, which directly accelerates development productivity — closed-source DXPs can't benefit from this in the same way. The brief asked for universal, not niche. That's what this is.

### A17's relationship with Twill

A17 created Twill, maintains it, and has deployed it across a range of clients and project types with comparable content complexity — the International Energy Agency, Open Society Foundations, the Guggenheim, and the National Academies among them. We've shipped production work on it for years. Twill isn't A17-only — it's open source with an active community used by other agencies and development teams. The codebase is public. The development approach is standard Laravel.

---

## 6. Architecture: Composable Model

The architecture is composable. The CMS handles content modeling and editorial workflows. Search, media delivery, CRM routing, consent management, and analytics are each handled by dedicated services connected through an orchestration layer that A17 builds and the firm owns.

### MVP Service Map

| Layer | Solution | Notes |
|---|---|---|
| CMS | Twill on Laravel | Content modeling, editorial workflows, block editor, media library, taxonomy |
| Search | Meilisearch | Self-hosted, includes AI capabilities, no SaaS procurement required |
| Media delivery | Twill native media library | Image optimization via Cloudflare |
| Forms | Centralized form handling | Routes to each firm's CRM through Laravel's queue system |
| Hosting | Upsun Dedicated | Contract passes through A17 |
| CDN / Security | Cloudflare | Already in use by both firms |
| Accessibility monitoring | Siteimprove | Already in use |

External SaaS dependencies at launch: Cloudflare and Siteimprove only. Both pre-existing. Hosting and CDN run on Upsun and Cloudflare — proven platforms with established security compliance and enterprise track records.

### Phase 2 Roadmap

The composable architecture is designed so each post-launch capability plugs in through its own service layer, on its own procurement timeline:

| Capability | Approach | Procurement dependency |
|---|---|---|
| **Managed search + analytics** | Algolia or Meilisearch Cloud (data model and index schema designed for this from Day 1; migration is a driver swap, not a rearchitecture; both Meilisearch and Algolia support AI-powered search — the move is about offloading hosting and gaining search analytics, not gaining AI capabilities) | Service contract at point of adoption |
| **DAM integration** | Media library is abstracted so a platform like Bynder plugs in by changing where the service points | DAM contract at point of adoption |
| **Deeper CRM integration** | Potentially consolidated across firms | Scoped post-launch based on firm decisions |
| **Multilingual expansion** | WS would prioritize Spanish and Portuguese | Content production, not platform work |
| **Content personalization** | Experimentation layer connects via middleware | Service contract at point of adoption |
| **Content syndication** | Distribution automation through API layer | Scoped post-launch |

None of these require changing the CMS or renegotiating a vendor contract.

---

## 7. AI and AEO Readiness

Both firms raised AI readiness in discovery. This section documents the technical basis for the claims in the executive summary.

**Server-side rendering and structured data** — Twill on Laravel renders pages server-side with structured data markup. AI agents and answer engines can consume this content directly — no client-side JavaScript assembly required for content to be indexable. This is the foundational requirement for AEO.

**Middleware flexibility** — Laravel's middleware layer can route requests through any AI service with an API. This means the architecture can accommodate AI-powered features (search, personalization, content recommendations) without rearchitecting the content delivery path.

**Content hub pages** — Both Holly and Mark described the need for pages around emerging topics (AI regulation, COVID response, the Crown Act). These are a Day 1 architecture feature, not a Phase 2 request. The content model supports ad-hoc tagging and dynamic aggregation natively. New topic hubs can be created by editorial teams without developer involvement.

**Structured data layer** — Content is structured and semantically tagged from the data model up, making it immediately available to answer engines and AI-powered search interfaces.

---

## 8. Lock-In and Portability

**Content model ownership** — Defined in code that A17 writes and the firm owns. Not stored in a proprietary schema.

**Data portability** — PostgreSQL with a standard relational schema. Data exports cleanly through standard tooling.

**Technology transferability** — Built on Laravel (MIT license, one of the most widely adopted PHP frameworks). Editorial workflows, block editor, media library, and taxonomy system are all standard Laravel patterns. If circumstances change, the technology is transferable.

**Frontend independence** — Standard web technology. No proprietary frontend framework or rendering pipeline.

**Architectural independence** — A17 will continue as the technology partner — that's the plan. But the architecture doesn't require it. That's a principle we build around.

---

## 9. Operating Model

The operating model both firms described in discovery — A17 owns hosting, manages the deployment pipeline, handles infrastructure, continues under maintenance retainer — is exactly how A17 delivers Twill projects. This is a white-glove engagement.

- Hosting: Upsun Dedicated, contract through A17
- CI/CD pipeline: A17-managed
- Monitoring: A17-managed
- Security posture: A17-managed, on proven, security-compliant infrastructure (Upsun + Cloudflare)
- Maintenance retainer: A17

One relationship, one team, accountable for the whole stack. No separate vendor relationships to manage. That's what both firms said they wanted.

---

## 10. Sources and References

### Platforms

- **Twill** — [https://twillcms.com](https://twillcms.com) | [GitHub](https://github.com/area17/twill)
- **Laravel** — [https://laravel.com](https://laravel.com)
- **Optimizely** — [https://www.optimizely.com](https://www.optimizely.com)
- **Payload CMS** — [https://payloadcms.com](https://payloadcms.com)

### MVP Services

- **Meilisearch** — [https://www.meilisearch.com](https://www.meilisearch.com)
- **Upsun** — [https://upsun.com](https://upsun.com)
- **Cloudflare** — [https://www.cloudflare.com](https://www.cloudflare.com)
- **Siteimprove** — [https://www.siteimprove.com](https://www.siteimprove.com)

### Phase 2 Services

- **Algolia** — [https://www.algolia.com](https://www.algolia.com)
- **Meilisearch Cloud** — [https://www.meilisearch.com/cloud](https://www.meilisearch.com/cloud)
- **Bynder** — [https://www.bynder.com](https://www.bynder.com)

### Design System

- **Vitrine (A17)** — Internal; referenced as the component library and design system that ships with A17's Twill projects

### A17 Twill Portfolio (Comparable Complexity)

- **International Energy Agency (IEA)** — [https://www.iea.org](https://www.iea.org)
- **Open Society Foundations** — [https://www.opensocietyfoundations.org](https://www.opensocietyfoundations.org)
- **Guggenheim** — [https://www.guggenheim.org](https://www.guggenheim.org)
- **National Academies** — [https://www.nationalacademies.org](https://www.nationalacademies.org)

### Discovery Inputs

- TW discovery responses (requirements, integration landscape, IT preferences)
- WS discovery responses (requirements, integration landscape, IT preferences)
- Combined requirements matrix
- Integration audit (Vuture, OnePlace, Nexl, Foundation)
