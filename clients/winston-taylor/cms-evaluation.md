---
type: concept
title: CMS Evaluation
description: AREA 17 comparative CMS analysis and weighted scoring behind the Twill recommendation for Winston Taylor.
tags:
  - client
  - winston-taylor
  - area17
---
# CMS Evaluation

*Project Meridian | AREA 17 Technology | February 2026*

We evaluated three CMS platforms, each representing a different architectural approach. What follows is the comparative analysis behind the recommendation, including why we looked at Optimizely and Payload and where they fall short against this project's specific requirements.

## Platform Comparison

| Dimension | Laravel Twill | Optimizely | Payload CMS |
|---|---|---|---|
| Architecture | Composable, open source | Enterprise DXP, SaaS | Headless, open source |
| License | Apache 2.0 / MIT | Commercial, multi-year | MIT |
| Time to start | Immediate | 4-8 weeks (procurement) | Immediate |
| Annual licensing | $0 | $36K-$200K+ | $0 |
| Editorial experience | Built-in block editor, media library, workflows | Strong out-of-box | Requires custom frontend dev |
| Data architecture | PostgreSQL, relational | Proprietary schema | MongoDB-native (PostgreSQL adapter maturing) |
| AREA 17 production depth | Jointly maintains Twill | Certified partner available | Active but limited (ElevenLabs) |
| Developer ecosystem | Laravel, millions worldwide, extensive LLM training data | .NET, smaller talent pool | Next.js / React |
| Lock-in risk | None, standard schema, portable data | High, proprietary, auto-renewing contracts | Low, but Figma acquisition adds uncertainty |
| May 1 feasibility | Yes | No | Possible, higher risk |

## Laravel Twill

Twill's core strength is structured content modeling for editorial-heavy, taxonomy-driven sites. Professional directories cross-referenced with capabilities, offices, sectors, insights, and multilingual variants, that's the use case it was designed for. The block editor gives editorial teams the flexible templating the brief described. The media library handles bulk operations, responsive cropping, and image optimization natively. Role-based access control handles governance across two editorial teams.

The architecture is composable: the CMS handles content, everything else connects through a service layer. For the MVP, that means Meilisearch for search (self-hosted), Twill's native media library with optimization via Cloudflare, form handling that routes to each firm's CRM, and hosting on Upsun Dedicated with the contract through AREA 17. The hosting relationship is a white-glove offering: Upsun and Cloudflare are proven, security-compliant platforms, and both sit under the AREA 17 engagement.

AREA 17 jointly maintains Twill and has shipped production work at this scale for the International Energy Agency, Open Society Foundations, the Guggenheim, and the National Academies. LLMs are trained extensively on Laravel's open documentation and source code, which directly accelerates development productivity in ways closed-source platforms can't benefit from.

## Optimizely

Optimizely is a strong enterprise DXP. It came up in the brief as a platform of interest, and we took that seriously. The challenge is fit, not quality:

- Procurement runs 4-8 weeks minimum (license negotiation, contract review, partner coordination), which alone exceeds the timeline to May 1
- Pricing starts around $36K annually, scales above $200K for this content scale, on multi-year auto-renewing contracts
- Proprietary content schemas create vendor dependency both IT teams said they want to avoid
- The integration model assumes deeper buy-in to the Optimizely ecosystem over time
- Both IT teams described wanting an agency-managed operating model, not a vendor-managed DXP

## Payload CMS

Payload is a modern headless CMS on Next.js, and AREA 17 has real production experience with it (we're actively building on it for another client). It's open source, the developer experience is strong, and it's gaining traction for good reason. The gaps are specific to this project:

- **Platform maturity** — Payload is a rapid CRUD builder for Next.js, not a mature CMS with the editorial depth this project requires. Flexible templates, modular blocks, self-service management, media library with bulk operations, all of that requires significantly more custom frontend development than a platform where those workflows are built in.
- **Database fit** — originally architected around MongoDB, with a PostgreSQL adapter that's still maturing. This project's deeply relational content model (thousands of professional profiles cross-referenced with capabilities, offices, sectors, multilingual variants) is better served by PostgreSQL natively.
- **Strategic uncertainty** — Figma's recent acquisition of Payload introduces questions about long-term platform direction that didn't exist six months ago.
- **Production limits** — AREA 17 pushed Payload to its limits on ElevenLabs, a simpler site than this project. Our deepest institutional knowledge, production tooling, and design system (Vitrine) all live in the Twill/Laravel ecosystem.

## Post-Launch Roadmap

Each capability plugs in at the point of adoption, not before launch:

- **Meilisearch AI integration** — index schema and data model designed for this from Day 1, Phase 2 activates Meilisearch's built-in AI capabilities for natural language search and analytics
- **DAM integration** — media library abstracted behind a service layer, a DAM plugs in by changing where the service points
- **Deeper CRM integration**, potentially consolidated across firms
- **Multilingual expansion** — WS would prioritize Spanish and Portuguese
- **Content personalization** and experimentation
- **Content syndication** and distribution automation

## AI Readiness

Both firms raised this in discovery. WS wants to prioritize answer engine optimization over traditional SEO. TW described AI-enhanced search and personalization as near-term goals.

Server-side rendered pages with structured data are what AI agents need to consume (no client-side JavaScript assembly required). Laravel's middleware layer routes requests through any AI service with an API. The content hub architecture Holly and Mark described (dynamic aggregation for topics like AI regulation and COVID response) is a Day 1 feature, not a Phase 2 request. The content model supports ad-hoc tagging and dynamic aggregation natively, with structured data making that content immediately available to answer engines.

## Lock-in and Portability

Twill doesn't create lock-in. The content model is defined in code that AREA 17 writes and Winston Taylor owns. Data lives in PostgreSQL with a standard schema. Everything runs on Laravel, one of the most widely adopted PHP frameworks in the world. If circumstances change, data exports cleanly, the content model is documented, and the frontend is standard web technology.

## Operating Model

The operating model both firms described (AREA 17 owns hosting, manages deployment, handles infrastructure, continues under retainer) is exactly how we deliver Twill projects. Upsun Dedicated and Cloudflare are a white-glove hosting setup, proven and security-compliant, with the contract passing through AREA 17. One relationship, one team, accountable for everything.

We can do a quick demo of the CMS we already tailored and delivered in Week 1. Seeing the software firsthand would likely help the team realize what's possible and get comfortable with how intuitive the editorial experience actually is.
