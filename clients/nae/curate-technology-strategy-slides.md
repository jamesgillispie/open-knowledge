---
type: note
title: Curate Technology Strategy Slides from Existing Repository
description: Brief for evaluating, trimming, and reordering a repository of past AREA 17 technical strategy slides against the NAE Technology Strategy outline.
tags:
  - client
  - nae
  - bd
  - area17
---
# Curate Technology Strategy Slides from Existing Repository

I have two files attached:

1. **A .pptx slide deck** containing a repository of technical strategy slides from past AREA 17 projects. These are real slides from previous pitches and proposals that our managing director pulled together as the most relevant to our current project. There may be 30, 50, 100+ slides in here — the quantity varies.

2. **nae-technical-strategy-approach.md** — A technical strategy memo that outlines our approach for a specific proposal (NAE website redesign and CMS modernization). This is the content backbone.

## What I need you to do

Go through every single slide in the .pptx deck and evaluate each one against the Technology Strategy outline below. For each slide:

- If it maps clearly to a section in the outline, **keep it** and note which section it belongs to.
- If it's partially relevant but needs modification (wrong client name, slightly off-topic but close), **keep it** and flag what needs changing.
- If it doesn't map to anything in the outline, **delete it**.

Then **reorder the remaining slides** to match the outline's sequence. If a section in the outline has no matching slide from the repository, insert a blank slide with a text box noting what needs to be created (e.g., "NEEDS SLIDE: Migration feasibility assessment — see outline section 01.06").

## The Outline

The deck follows a three-section structure. The breadcrumb format for each slide should be "Technology strategy / [Section Name]".

### Section 01: Technical Discovery and Assessment

Breadcrumb label: Discovery

1. **Overview** — We start by understanding what exists, what works, and what's holding you back. (Look for: slides about discovery methodology, technical audit process, assessment frameworks)
2. **Platform and stack audit** — Evaluating existing technology, CMS capabilities, hosting, and technical debt. (Look for: Wappalyzer outputs, stack analysis, technology assessments, legacy platform reviews)
3. **Integration mapping** — Documenting APIs, data sources, authentication layers, third-party services. (Look for: ecosystem diagrams, integration maps, system architecture overviews, API inventories)
4. **Content and data modeling** — Assessing how content is structured, stored, and related. (Look for: content model diagrams, entity relationships, CMS content type documentation, data architecture)
5. **Performance and security baseline** — Establishing measurable baselines for speed, accessibility, and security. (Look for: Lighthouse scores, Core Web Vitals, security audits, accessibility reports, performance dashboards)
6. **Migration feasibility** — Evaluating export capabilities, content volume, transformation complexity. (Look for: migration planning slides, content audit results, data extraction methodology, migration pipelines)

### Section 02: Architecture and Technical Planning

Breadcrumb label: Architecture

1. **Overview** — We design systems that solve today's problems without creating tomorrow's constraints. (Look for: architecture methodology slides, technical planning frameworks, decision-making process)
2. **CMS and platform selection** — Recommending the right CMS based on editorial needs and long-term maintainability. (Look for: CMS comparison slides, platform recommendation frameworks, Twill/Laravel/Craft/Drupal evaluations, editorial workflow demonstrations)
3. **Search and discoverability** — Designing search infrastructure, federated search, AI-enhanced relevance, SEO/GEO strategy. (Look for: search architecture diagrams, SEO strategy slides, search engine comparisons, discoverability frameworks)
4. **API strategy and integration design** — Defining how the platform communicates with external systems. (Look for: API topology diagrams, integration architecture, data flow diagrams, system boundary definitions)
5. **Scalability and multi-site readiness** — Architecting for growth without overbuilding. (Look for: multi-site architecture, shared component systems, governance models, platform scalability slides)

### Section 03: Delivery and Risk Management

Breadcrumb label: Delivery

1. **Overview** — We scope honestly, build iteratively, and test continuously. (Look for: delivery methodology slides, agile/sprint process, project risk frameworks)
2. **Honest scoping and phased delivery** — Defining achievable scope within real constraints, separating core from future phases. (Look for: phased roadmaps, scope definition slides, timeline planning, MVP/phased delivery frameworks)
3. **Content migration execution** — Automated tooling plus manual QA at scale. (Look for: migration pipeline diagrams, content migration methodology, QA validation workflows, redirect strategies)
4. **Accessibility and compliance** — WCAG 2.2 AA and Section 508 as a first-class workstream. (Look for: accessibility testing methodology, WCAG compliance slides, screen reader testing, automated scanning workflows)
5. **DevOps and launch readiness** — CI/CD pipeline, environment parity, monitoring. (Look for: DevOps pipeline slides, CI/CD diagrams, deployment workflows, monitoring setup, environment architecture)
6. **Long-term sustainability** — Warranty, ongoing maintenance, knowledge transfer. (Look for: support model slides, warranty scope definitions, retainer frameworks, training and handoff methodology)

## How to handle edge cases

- **Slides that are good but reference a different client:** Keep them, flag the client name that needs swapping. Don't rename yet — just note it.
- **Slides that cover two outline topics on one slide:** Keep them, note they may need to be split or that they cover multiple sections.
- **Multiple slides that could work for the same outline section:** Keep all of them and note the options. I'll pick which one to use.
- **Slides with great visuals but wrong/generic body text:** Keep them, note "visual is good, body text needs rewrite for NAE context."
- **Section divider or transition slides from past decks:** Keep any that match the dark-navy-background overview style. Delete generic title slides that don't carry content.

## Output format

After you've processed the deck, give me a summary that looks like this:

**Kept:** [X] slides **Deleted:** [X] slides **Gaps (need new slides):** [list which outline sections have no matching slide]

Then walk me through the reordered deck slide by slide, noting:

- Slide number (new position)
- Original slide number (for reference)
- Which outline section it maps to
- Status: Ready / Needs text update / Needs client name swap / Visual good but text needs rewrite / etc.
- Any notes

Save the reordered, trimmed .pptx as the output file.
