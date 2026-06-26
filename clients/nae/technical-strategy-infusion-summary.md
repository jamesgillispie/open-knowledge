---
type: note
title: NAE Technical Strategy Infused — Summary
description: Summary of the slide-by-slide updates that wove NAE-specific technical strategy through the deck, plus items still needing manual attention.
tags:
  - client
  - nae
  - bd
  - area17
---
# NAE Technical Strategy Infused — Summary

The content is solid. The architecture overview explicitly references NAE's integration landscape, the NASEM codebase advantage, and all key systems.

Here's the complete summary of what was done:

---

## NAE Technical Strategy Infused — Complete

### What I Updated

**Title & Framing (2 slides)**

- **Slide 1**: "NASEM Technology approach" → "NAE Technology strategy". Removed section number "4". (Note: the header image still reads "AREA 17 × NASEM" — this is an image file your team needs to swap.)
- **Slide 2**: Intro text now references NAE specifically and the NASEM experience advantage.

**Gap Slides — All 6 Rewritten with NAE Strategy (slides 3, 11, 12, 13, 41, 42)**

- **Slide 3** (Discovery Overview): References NASEM head start, ACMS export unknowns, NAE content volume (8,000+ profiles, 1,748 tributes, 500+ news items), and integration mapping for Impexium/Informz/Higher Logic.
- **Slide 11** (Content & Data Modeling): Covers NAE vs NASEM content model differences — CMS-native vs orchestrated from source systems, Pathways Into Engineering content, Engineering Career Atlas taxonomy.
- **Slide 12** (Migration Feasibility): Two-track plan (structured export vs AI-assisted scraping), specific content volumes, 13,000+ URL redirect strategy from flat nae.edu/312274.aspx structure.
- **Slide 13** (Architecture Overview): NASEM fork-ready codebase, NAE-specific integration landscape (NAP, Impexium, Okta, Informz, Higher Logic), competitive positioning.
- **Slide 41** (Delivery Overview): May-to-December timeline reality, NASEM lessons learned, Phase 1 vs Phase 2 framing.
- **Slide 42** (Honest Scoping): Explicit Phase 1 (December launch) scope and Phase 2 (Pathways, Career Atlas, Wayfinder) breakdown.

**Architecture & Integration Slides (slides 8-10, 14-15, 40)**

- Architecture I-III: Rewritten for NAE's integration landscape (Impexium, NAP, Okta, Informz, Higher Logic)
- Infrastructure diagram: Updated from NASEM sources to NAE integrations
- Service gateway: Updated labels from "NASEM" to "NAE", source systems from "NAP/NAPAR/PoolParty" to "NAP/Impexium/Okta/Informz"

**Search & Discoverability (slides 28-29, 33)**

- Search: Complete rewrite — now proposes Typesense/Meilisearch with AI semantic layer, federation with NAP, editorial control
- SEO: Rewritten around NAE's 13,000+ URL redirect strategy, semantic URL architecture, Pathways consolidation future-proofing
- Emerging Tech: Reframed for NAE's AI-enhanced search requirement and migration automation

**CMS & Platform (slides 19, 23, 25, 35)**

- Twill/Open Source: Now references NASEM as fork-ready foundation, proven NAP integration
- Headless: Reframed for NAE's Pathways consolidation (EngineerGirl + EngineerTeen)
- Headless experience: References Phase 2 initiatives (Career Atlas, Wayfinder, Higher Logic)
- Design system: "NAE's design system adapts the proven NASEM component library"

**Performance & Accessibility (slides 5-6, 45)**

- Performance: Framed as NAE baseline targets, not generic principles
- Accessibility: WCAG 2.1 → WCAG 2.2 AA + Section 508, references NASEM lesson that testing takes longer than expected, QA as first-class phase
- Four pillars: Updated WCAG reference

**Scalability & Sustainability (slides 34, 40, 47-48)**

- Scale: Reframed for Phase 1 → Phase 2 architecture
- Gateway: Now names all NAE services (Impexium, NAP, Informz, Okta)
- Hosting: Title updated for NAE CI/CD context
- Sustainability: "NAE's platform must be resilient, maintainable, and ready for Phase 2"

**Migration (slide 43)**

- Intro rewritten with NAE ACMS specifics, content volumes, AI-assisted migration tooling advancement

### Key Strategic Threads Woven Throughout

1. **NASEM codebase = fork-ready foundation** (not just a reference project)
2. **NAP integration already built** — configurable for NAE's catalog
3. **Two-track migration plan** for ACMS uncertainty
4. **Phase 1 / Phase 2 honest scoping** — December is credible if we scope right
5. **AI-enhanced search** — specific stack recommendation (Typesense/Meilisearch + semantic layer)
6. **13,000+ URL redirect** strategy planned from day one
7. **WCAG 2.2 AA + Section 508** — QA as a first-class phase, not a buffer

### Still Needs Manual Attention

- **Slide 1 header image**: "AREA 17 × NASEM" is an embedded image — needs to be swapped to "AREA 17 × NAE"
- **Diagram visuals** on slides 8-10, 14-15: The architecture diagrams themselves are images — text labels around them are updated but the embedded diagram graphics still show generic/Lucas/NASEM system names
- **6 gap placeholder slides** (3, 11, 12, 13, 41, 42): Content is written but they're plain text on white. Your design team needs to format these in the dark-navy section divider style
