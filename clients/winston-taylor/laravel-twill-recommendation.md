---
type: concept
title: Laravel Twill Recommendation
description: AREA 17 technical write-up on recommending Laravel Twill for the Winston Taylor MVP, with stack and roadmap.
tags:
  - client
  - winston-taylor
  - area17
---
# Laravel Twill Recommendation

*Project Meridian | AREA 17 Technology | February 2026*

After 2 weeks of fast-paced discovery, AREA 17's recommended CMS for the new Winston Taylor website is Laravel Twill. We evaluated your requirements through our detailed audit and questionnaire, and the biggest takeaway is that the hardest constraint isn't content complexity or editorial workflow, it's the May 1 deadline tied to the merger announcement. There's no backup option and no room for negotiation on that date.

Twill fits here precisely because of that constraint. AREA 17 jointly maintains Twill and has shipped dozens of production sites on it, including sites with comparable content complexity and editorial team size. And because Twill is open source (Apache 2.0 for Twill, MIT for Laravel), there's no vendor procurement cycle, no license negotiation, no contract review to get through before work starts. The dev environment goes up the day the stack is approved.

That said, if May 1 were six months away, we'd still recommend Twill. The architecture is right for what the Winston Taylor digital platform needs to become.

## Guiding Principles

These principles surfaced in discovery with both firms' leadership and IT teams:

- **No vendor dependency**, both firms want an agency-managed model, not a multi-year DXP contract with proprietary schemas and escalating license fees.
- **Composable by design**, the CMS handles content and editorial workflows, everything else (search, media, CRM routing, analytics) plugs in through a service layer that AREA 17 builds and Winston Taylor owns. If a better search product ships, you swap the search driver. If CRM consolidation happens next year, the form routing layer gets a new endpoint, not a new architecture.
- **Open source, universal code**, Twill is Apache 2.0, Laravel is MIT. The developer ecosystem is in the millions, the codebase is public on GitHub, and LLMs are trained extensively on Laravel's open documentation, which directly accelerates development in ways closed-source platforms can't match.
- **Timeline-compatible**, no procurement cycle, no license negotiation, no contract to finalize. We start building the day the stack is approved.

Twill also doesn't create lock-in. The content model is defined in code that AREA 17 writes and Winston Taylor owns, data lives in PostgreSQL with a standard schema, and the frontend is standard HTML, CSS, and JavaScript. If circumstances change, the path forward is manageable.

## MVP Stack

For launch, the stack is lean by design. AREA 17 manages the full hosting relationship through our agency partnership with Upsun, who handles infrastructure, while Cloudflare handles CDN and security (both proven, security-compliant platforms that IT teams on both sides can align around). The contract passes through AREA 17, so it's one team, one relationship, accountable for the whole thing.

| Component   | Solution                     | Notes                                              |
| ----------- | ---------------------------- | -------------------------------------------------- |
| CMS         | Laravel Twill                | Open source, AREA 17-maintained                    |
| Search      | Meilisearch                  | Self-hosted, no SaaS procurement                   |
| Media       | Twill native library         | Responsive crops, WebP optimization via Cloudflare |
| Forms / CRM | Laravel queue routing        | Vuture (TW), Nexl (WS)                             |
| Hosting     | Upsun Dedicated + Cloudflare | White-glove, managed through AREA 17               |
| Analytics   | Siteimprove / GTM, GA4       | Already in use                                     |

## Post-Launch Evolution

Both firms described a digital presence that's going to evolve significantly post-launch. AI-enhanced search, content personalization, CRM integration depth, multilingual expansion, gated content strategies. Some of those needs are well-defined today, others will emerge as the merged firm finds its footing (my hunch is the post-MVP roadmap will look pretty different a year from now than what either firm imagines today). The CMS decision isn't just about what gets built in eight weeks, it's about whether the platform makes the next two to three years of evolution possible without starting over.

The composable architecture means each new capability plugs in at the point of adoption, not before launch:

- **Meilisearch AI integration**, the index schema and data model are designed for this from Day 1, Phase 2 activates Meilisearch's built-in AI capabilities for natural language search and analytics
- **DAM integration** (Bynder or similar) when asset volume and cross-firm publishing justify it
- **Deeper CRM integration**, potentially consolidated across firms
- **Multilingual expansion**, WS would prioritize Spanish and Portuguese
- **Content personalization** and experimentation
- **Content syndication** and distribution automation

None of these require changing the CMS, renegotiating a vendor contract, or retraining editorial teams. Each one plugs in rather than requiring a rebuild.

## Due Diligence

AREA 17 has shipped Laravel Twill at comparable scale and content complexity for the International Energy Agency, Open Society Foundations, the Guggenheim, and the National Academies.

If questions remain we can do a quick demo of the CMS we already tailored and delivered in Week 1. Seeing the software firsthand would likely help the team realize what's possible and get comfortable with how intuitive the editorial experience actually is.

## Appendix A: Security and governance

SOC 2 compliance came up in the Feb 25 session as a hard requirement, and SSO integration with Azure AD/MFA was discussed alongside it. The security questionnaire process is already initiated. Both IT teams need to vet the stack, and this was a consistent theme across multiple meetings that directly shaped our evaluation criteria. The stack was chosen with this in mind (Upsun and Cloudflare are both proven, security-compliant platforms that give both IT teams something concrete to align around).

## Appendix B: AI and AEO readiness

Both firms raised this in discovery, not as a Phase 2 nice-to-have but as a design constraint from Day 1. WS wants to prioritize AEO over traditional SEO, TW described AI-enhanced search as near-term. The Feb 16 meeting had extended discussion about structuring the content model to be machine-readable from launch. This is baked into how we're thinking about the content architecture, not bolted on later.

## Appendix C: No throwaway work

The Feb 16 session had the explicit framing: "we don't want to build something and then just throw it out and start over." This shaped the composable architecture argument and is worth calling out on its own. Every decision in this stack is designed to carry forward, nothing here is scaffolding that gets torn down in a future phase.

The [CMS Evaluation](/clients/winston-taylor/cms-evaluation.md) doc has the full comparative analysis and weighted scoring.
