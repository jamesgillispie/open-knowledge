---
type: note
title: OSI Website Redesign — SOW and Project Context
description: Open Society Institute (OSI/OSF) website redesign project context, memory, and the full draft Statement of Work (V01D01).
tags:
  - client
  - osf
  - area17
---
# OSI Website Redesign — SOW and Project Context

All projects OSF new BD to help refresh designs for a long time existing A17 client

## Project context & memory

Start a task in Cowork SOW technical review and scoping Last message 14 seconds ago Refining SOW technical architecture paragraph Last message 20 days ago CMS generic page module scope review Last message 27 days ago Technical architecture and implementation planning Last message 2 months ago Memory Only you

**Purpose & context** James is a Technical Director at A17 working on complex web development projects, particularly website redesigns and technical implementations for clients like the Open Society Foundation (OSI). His primary role involves reviewing and refining Statements of Work (SOW), conducting technical due diligence, and ensuring project scope is properly defined to prevent budget overruns and scope creep. He collaborates closely with project managers like Dominique and works within a team structure that includes colleagues like Dom and Luke. James focuses on translating business requirements into accurate technical specifications while maintaining appropriate formality for client-facing documentation.

**Current state** James is actively working on multiple SOW documents that require technical validation and refinement. He's currently navigating project boundaries between new development work and existing maintenance programs (like Care programs), ensuring clear separation of responsibilities. Recent work has involved auditing existing codebases using tools like Claude Code to validate technical feasibility within budget constraints, particularly around Twill CMS implementations and content block reusability. He's also managing security protocols around repository access and credential management within the team's shared systems.

**Key learnings & principles** James has developed strong expertise in identifying technical risks early in the project scoping phase, particularly around CMS upgrades where version specificity and migration complexity can significantly impact budgets. He's learned that vague technical requirements in SOWs often lead to scope creep, making detailed technical discovery sessions essential before finalizing client agreements. His experience shows that modular content block architectures tend to be more reusable than relationship-based blocks, and that "latest version" upgrade language can hide significant migration complexity that should be scoped separately.

**Approach & patterns** James follows a systematic approach to SOW review that includes flagging incomplete technical specifications, identifying missing requirements sections, and conducting codebase audits to validate proposed timelines. He collaborates with Claude to refine both technical content and appropriate tone for different contexts - maintaining formal SOW language for client documents while ensuring technical specificity. His workflow includes creating structured technical discovery sessions, establishing scope validation checkpoints, and providing clear rationale for technical decisions to team members through inline comments and explanations.

**Tools & resources** James works extensively with Twill CMS, PHP, Laravel, and modern web development stacks including npm and Composer package management. He uses Claude Code for codebase auditing and technical due diligence, and relies on shared credential management through 1Password for team access to client repositories. His technical review process involves GitHub repository analysis and he maintains awareness of security protocols around repository access and credential usage.

Last updated 20 days ago

Instructions Add instructions to tailor Claude’s responses

Files 1% of project capacity used

SOW _ AREA17_OSI_Website_V01D01.md 392 lines

SOW _ AREA17_OSI_Website_V01D01.md 24.05 KB •392 lines • Formatting may be inconsistent from source

---

# Statement of Work

# Open Society Institute

Website redesign

| Draft Client version 01 | Last updated Nov 20, 2025 | |
|---|---|---|
| | | |
| Prepared by AREA 17 Citrine Ghraowi  Dominique Deriaz | Presented to Open Society Institute  Chipp Winston | |

# Table of contents

- [Table of contents 2](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.meyukshapg6z)
- [Partnership 4](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.68mn8qdxgysh)
- [Preface 4](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.4lbthmwyr3c5)
- [Approach 5](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.cl3t0j3bm6ji)
- [Overview 5](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.9n4cjf552hhd)
- [Set-up 5](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.gk2p4p5f0x7u)
- [Ideation 6](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.2pijb7ob01z1)
- [Foundation 7](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.79te7lvkktnz)
- [Implementation 8](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.bgzgt9ql38rc)
- [Implementation sprints 8](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.h48tfbigumim)
- [Deployment 9](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.jdoxkn78a1pv)
- [Client responsibilities and obligations 11](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.bkpos3hrxmkm)
- [Communication and status 12](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.ar62te7f0s01)
- [Process 14](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.x2bdwh3z7unh)
- [Period of performance 14](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.cd3v5v920d9y)
- [Team 14](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.uizgxysuk673)
- [Fees 15](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.x5czgm5u60wn)
- [Payment schedule 15](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit?tab=t.0#heading=h.hu8e0hjy3kv5)
- [Annex (optional) 18](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit#heading=h.sxc4lys2jdxb)
- [Business requirements 18](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit#heading=h.y07357re12pp)
- [Features, integrations and screen views 18](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit#heading=h.ix1ep5xinyo9)
- [3rd party integrations 20](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit#heading=h.28a8bna1scur)
- [Screen views 21](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit#heading=h.q3eeaauux8mc)
- [Technical requirements 22](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit#heading=h.dmury2u4cr8q)
- [Coding languages and frameworks 22](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit#heading=h.z8mf021lo94u)
- [Server environments 22](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit#heading=h.kfr116d0dpra)
- [Hosting and deployment services 23](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit#heading=h.ynv104e6x1m)
- [Other 3rd party services 23](https://docs.google.com/document/d/1QDdNIHH1wt0BHoVxGpm0xrIIc3E5cOX2V7r5g8PireA/edit#heading=h.wkb0ac93kths)

# Partnership

## Preface

This Statement of Work (“SOW”) between Area 17 Media, LLC (“AREA 17”) and Open Society Institute  (“Client”) is hereby connected to the Master Services Agreement (“Master Agreement”) between the parties delivered November 28, 2025. All terms used, but not defined herein shall have the meanings set forth in the Master Agreement.

# Approach

## Overview

To support Open Society Institute (OSI) in modernizing their website and aligning it with their refreshed brand and organizational goals, AREA 17 will utilize a phased process built on clarity, collaboration, and iterative alignment.

As part of our earlier phases, we determined a two pronged approach to redesigning the site. Some sections will be completely re-imagined (specific landing pages, Voices experience) vs. others will be “re-skinned” (back-end str

## Set-up (1 week)

We aim to set each project up for success by establishing a shared set of principles and guidelines for effective communication and collaboration. In the intervening weeks prior to project kickoff, we will assemble all of the pertinent information, documentation, schedules, and activities necessary for our forthcoming collaboration and combined success.

**Client inputs**

As we prepare for a successful project kick off, AREA 17 will require the following activities, documentation, or preparation from CLIENT:

- List of important internal dates, scheduling conflicts, stakeholder details, dependencies, etc.
- List of any adjacent vendors or teams that will be expected collaborators or stakeholders, as relevant (e.g. accessibility team, copywriter,strategic partners, local teams, etc.)
- Names and titles for full client team and stakeholders; contact list for core team members
- Initial hand-off of materials and preparation, as aligned upon with project managers
- Research materials from internal audits
- List of communication or project management software used and any requirements for use on this project, as relevant
- Technical documentation and access to existing development environments and codebase(s)
- Logistics alignment before project kick-off, including introduction to Procurement/bookkeeping, signed documentation, confirmation of invoice schedule, etc.

**Workstream detail**

| Activities | Outcomes |
|---|---|
| Partner onboarding:  Upon signature, your primary AREA 17 contact will introduce you to your project leadership team, and welcome and onboard you to your partnership with AREA 17. | Introduction to Project team Establishing the project experience |
| Project set-up:  Leading up to the project kickoff, AREA 17 Producer works with Client to finalize project planning and operations including collaborative process, team, timelines, milestones and preliminary scheduling. | Shared core team contact list and shared Slack channel (as relevant) Updated schedule and scope, as relevant Production kick off, including collective next steps |
| Project kick-off:  AREA 17 conducts a kick-off with Client to introduce the project, including the logistical and strategic goals, roles and responsibilities, and a preliminary workshop to confirm begin to unpack business goals, user needs and competitive landscape at a high, setting pace for the project. | Kick off agenda, guiding deck and facilitation |
| Roadmap alignment planning: Scheduling alignment touchpoints at a regular cadence allows us to ensure our progress and prioritization, as well as proactively assessing any risks or opportunities in workstreams ahead. | Roadmap and priorities alignment touchpoints scheduling and cadence |

## Research (0 week, done)

To understand your organization and various audiences needs, Research was led as part of the Brand Evolution project, resulting in a Product brief for the website that was delivered and approved by OSF. This Product brief serves as a base for this SOW and will be the jumping board for the website project.

## Ideation (5 weeks + 2 weeks socialization)

This Ideation phase is more extensive than usual due to the breadth of reimagined sections and the content-driven nature of OSI’s website. Ideation will focuses on rethinking core experience areas—identified as navigation, storytelling landing pages, and the Stories experience—and establishing the structure and content model required to support them. For pages where content is not being rethought, we will retain the back-end data structure but explore new front-end experiences.

Ideation is divided into two sub-phases:.

- Phase 1 (2 weeks)  : The first focuses on structure and content, defining information architectureIA, content needs, and early narrative frameworks in close partnership with OSI and their copywriter. This ensures that content clarity precedes UX exploration. At the end of Ideation Phase 1, a one-week socialization period ensures organizational alignment before moving to UX.
- Phase 2 (3 weeks)  The second phase focuses on UX, producing wireframes and design concepts based on a clearly aligned content plan. At the end of Ideation Phase 2, a one-week socialization period ensures alignment on UX direction before entering Foundation.

Between these sub-phases, a socialization period ensures organizational alignment before moving to UX. A second socialization period ensures UX direction is aligned before entering Foundation.

By the end of Ideation, OSI will have a final website structure, a reimagined direction for key sections, rough mockups of the core areas of new experience, and a clear sense of how the new brand will be expressed digitally—ready to be matured into a complete system during Foundation.

**Workstream detail**

Client inputs are to be expected in this workstream and will be aligned upon in the workstream leading up and at scope alignment points where relevant.

| Activities to be confirmed | Outcomes |
|---|---|
| Part 1 Alignment on IA, content structures, and content needs through intake sessions Finalization of which parts of the back-end will remain the same vs. which parts will change Close collaboration with OSI copywriter to finalize narrative direction  Module audit to ensure future design coverage Part 2 UX exploration and wireframing, concept mockups for reimagined sections  Design exploration | Clear understanding of content priorities for reimagined sections (landing pages, stories) Defined site structure and aligned content model, including which parts of the back-end will stay the same and which will be re-architected Defined landing page direction, and Stories experience direction  Rough wireframes for reimagined sections (landing pages, stories) Aligned creative direction for digital expression of new visual ID for finalization in next phase |

## Foundation (6 weeks + 1 week of socialization)

In Foundation, we extend and refine the work from Ideation into a fully realized design system and UX architecture for the website. This includes designing key templates, specifying all UI components, and finalizing the digital expression of OSI's refreshed brand identity. Building from the rough mockups and structural decisions made in Ideation, we create a complete, scalable design language across desktop and mobile.

This phase also includes defining the technical architecture and requirements for implementation. The engineering team will validate assumptions, upgrade Twill to the latest version, outline CMS configuration, confirm third-party integrations, and prepare the development environment. The combination of product architecture, design system, and technical specification ensures that Implementation proceeds efficiently and with full transparency.

**Workstream detail**

Client inputs are to be expected in this workstream and will be aligned upon in the workstream leading up and at scope alignment points where relevant.

| Activities to be confirmed | Outcomes |
|---|---|
| Final design system including typography, color, layout and components  High-fidelity design of key templates and flows  UX foundation including finalized wireframes  Documentation of content architecture and navigation  Module and template specifications  Technical architecture requirements  CMS evolution specifications confirmation, including what's retained vs. restructured  Development environment setup and Twill upgrade preparation | Fully specified and aligned design system  Finalized UX and template specification ready for implementation  Validated technical plan for implementation  Stable development environment ready for implementation sprints |

## Implementation (11 weeks)

The Implementation phase brings the Foundation work to life through a series of two-week sprints. At this stage, engineering builds the website using the fully specified design system and technical architecture. Each sprint follows a prioritized roadmap, delivering tested, functional components, templates, and features. Because the number of required sprints depends on the final complexity defined during Ideation, we have budgeted for four sprints with the option to add more.

This phase includes front-end development, back-end development, and CMS configuration. Quality assurance, browser testing, and design validation occur continuously within each sprint.

### Implementation sprints (4 sprints of 2 weeks)

Implementation sprints are a way to organize and plan the overall effort of the project and coordinate a cross-disciplinary team to address components of the project in a prioritized sequence. Each sprint takes two weeks and begins by confirming and/or revising the priorities and requirements outlined in the product roadmap.

Within each two week sprint, a cross-disciplinary team tackles the challenges and requirements outlined in the product roadmap, extending the user experience and design system. In coordination with design, which will naturally be slightly ahead, the features of the CMS and application are built according to the technical specifications. Through a close integration of user interface and application development, the application is implemented and integrated with specified third party APIs.

Throughout each sprint, the user interface is tested for browser compatibility and the application for functionality (‘sanity’ testing). Within each sprint the integrated application is tested by both the client and the AREA 17 QA team (‘holistic’ testing).

| Activities to be confirmed | Outcomes |
|---|---|
| Platform core setup Twill upgrade and CMS configuration UI library setup Sprint planning Application development (back-end development) Coded website interface (front-end development) Holistic QA (design and functional) Security and load testing Production infrastructure configuration Launch planning and support | Continual alignment and clarity of priorities and progress Functional templates and flows delivered incrementally Tested, integrated components aligned to roadmap |

### Quality assurance and Deployment (3 weeks)

Following Implementation, we will have dedicated time for quality assurance and deployment of the website. As part of Implementation, we’ll uncover roles and responsibilities related to deployment. AREA 17’s standardnormal deployment process has the initial deployment scheduled according to the product roadmap, and happens across three phases: Alpha, during which the site is live but only accessible to the teams working on the project, Beta, during which the site is live to the public, but not marketed and Gold, after which the site is ready for prime time. During each of the deployment stages, the site is optimized for security, performance, and SEO.

During subsequent implementation sprints, deployment is incorporated into the sprint itself and accounted for in the product roadmap.

| Activities to be confirmed | Outcomes |
|---|---|
| Production infrastructure configuration Holistic QA (design and functional) Security testing Load testing Performance optimization Launch plan | Stable and performant website running in production Onboarded internal team able to take ownership of the technical and operational activities supported by the new infrastructure |

## Scope Assumptions

- Workday integration not included (will work as currently)
- Current translation functionality will be  retained
- The grant/fellow databases will be sunset

## Client responsibilities and obligations

Client is responsible for the following items:

**Throughout project**

- Two (2) day turnarounds on approvals and project requests unless otherwise mutually approved
- Single point of contact with full authority for all decisions/approvals (“Client Project Manager")
- Maintain active participation in scheduled meetings and workshops (virtual or in-person), providing input and feedback as needed to keep the project on track.
- Notify AREA 17 in writing of any change in key personnel, especially the designated Client Project Manager or primary stakeholders.
- Access to relevant decision-makers and stakeholders for approvals
- All other necessary materials requested during the project to be delivered on time
- Continuous project, no blackout periods. If a pause or blackout period is required, a project Amendment will be aligned upon and issued.
- Written response for all deliverables or activity feedback: Approvals should be provided in writing and specify whether the Deliverable is (a) approved with no changes (AREA 17 will proceed to the next Deliverable), (b) approved with comments (Client will give detailed comments in writing), or (c) not approved (Client will give detailed comments in writing). AREA 17 will make revisions based on comments provided to bring the Deliverable in line with Client feedback. Approved deliverables and milestones will not be altered after final acceptance unless both Client and AREA 17 agree to a change order in writing.

**User Experience and Design**

- Visual identity suited for digital use as relevant
- Sample assets and content required for design
- Typography and licensing costs for usage on Web ahead of development

**Content, Copy, Contribution**

- Messaging
- Content migration
- Copywriting, proofreading, and data entry as relevant
- Confirm final approval for content before integration into design and development phases.
- All assets in digital form (e.g. copy, logos, photography, video, etc.)
- Production of illustrations or visual assets, when needed.
- All applicable licenses and copyrights to materials provided to AREA 17 for use. Ensure that all content provided does not infringe on third-party intellectual property rights. Client assumes liability for any content they supply.
- Access to structured (JSON, or XML formats) and documented data sources for data migration (if applicable).

**Hosting, Infrastructure, DevOps**

- Provide the infrastructure that meets the project’s technical requirements approved during the project, prior to the beginning of development. This involves usage of cloud-based providers (Eg. AWS, GCP, etc) to create the necessary resources like servers, networking (load balancers), database, caching or similar services required by the project.
- All infrastructure and hosting costs related to the above-mentioned resources for development, staging, and production environments.
- Provide secure access to credentials, server login details, and necessary administrative rights for the development team to deploy the project codebase to the indicated resources.
- Manage domain registration and DNS configurations. Ensure proper routing on public networks (outside of client infrastructure) and within their secure connections (if applicable)
- Automate deployment tasks when possible and provide clear documentation of the deployment process.
- Set up and manage continuous integration/continuous deployment (CI/CD) pipelines to automate deployments (if applicable)
- Monitor infrastructure performance, activity logs and other metrics to flag possible issues to the project development team.
- Perform system maintenance and schedule the necessary software and hardware upgrades to keep the services operational and optimal.

**Third-party services**

- Provide access to third-party services accounts necessary for the development of the project, which meets the technical requirements approved during the project.
- All associated costs with those 3rd party services
- Provide credentials for those services that access cannot be provided (Eg. Google Analytics/Google Tag Manager property IDs)
- APIs of third-party solutions that are stable and ready for integration, along with the complete associated technical documentation
- Be responsible for renewing or maintaining ongoing licenses or subscriptions related to third-party tools, services, or data sources integrated into the project.

## Scope Assumptions

- Scope does not include integration with Workday integration not included
- Current translation functionality is retained
- The We are sunsetting all grant/fellow databases will be sunset

## Communication and status

Main points of contact: Prior to Project kick-off, Client and AREA 17 will determine one point of contact each. All decisions/approvals will be made through these two individuals. Client Project Manager will be the sole point of contact for Client and has full authority to speak for and sign-off on deliverables for Client.

Core project team: Prior to Project kick-off, Client will determine a ‘core project team’ including up to 5 people across the organization who may participate in core team meetings and workshops and is part of the Client’s feedback and decision-making team. While other individuals at the company may be consulted or involved, it is these individuals who are the project’s stakeholders and express involvement.

Standing meeting: A collaborative meeting will be held every week of the project and will include, at minimum, AREA 17 and Client Project Managers. Open opportunities and risks may be discussed at each meeting and/or meetings may be used for Client presentations, workshops or otherwise as aligned upon week over week.

# Process

## Period of performance

The Project is estimated to start in January 2026, Year, and complete in June, 2026. The estimated total period of performance is approximately X weeks as outlined in the below sample timeline. Please note that the final Project schedule and milestones will be established by the AREA 17 and Client Project Managers upon the project’s kickoff.

## Team

AREA 17 will dedicate team members during each phase of the project, who will be supported by the project leadership team which will consistently remain engaged throughout the course of the project. Fees are based on the duration of each phase at the estimated team allocations. Below is a breakdown of the projected allocations per phase.

| Role | Research | Ideation | Foundation | Implementation |
|---|---|---|---|---|
| Project team | | | | |
| Strategist | - | - | - | - |
| UX Designer | - | - | - | - |
| Designer | - | - | - | - |
| Interface Engineer | - | - | - | - |
| Application Engineer | - | - | - | - |
| Project leadership | | | | |
| Principal | - | - | - | - |
| Producer | - | - | - | - |
| Strategy Director | - | - | - | - |
| UX Director | - | - | - | - |
| Design Director | - | - | - | - |
| Technical Director | - | - | - | - |

## Fees

For the duration of the project, the associated team allocations and activities listed within this document, Client will pay AREA 17 the following amounts. If additional team members or activities are required, additional fees may be incurred. All overages and out-of-pocket expenses will be approved beforehand by Client.

**Project fees**

| Phase | Duration | Price |
|---|---|---|
| Set up | 1 week | $5,800 |
| Ideation | 5 weeks | $150,050 |
| Foundation | 6 weeks | $157,200 |
| Implementation | 11 weeks | $262,320 |
| Socialization | 32 weeks | $14,240 |
| TOTAL | 25 weeks | $589,600 |

## Payment schedule

Subject to the terms and conditions contained in this SOW and the Master Agreement, Client shall pay the AREA 17 fees in accordance with the following schedule:

PASTE/LINK TABLE FROM SHAPER (example below).

| Invoice 1 of | 10 | — | $194,902 | due on signature |
|---|---|---|---|---|
| Invoice 2 of | 10 | — | $92,322 | on August 1, 2021 |
| Invoice 3 of | 10 | — | $92,322 | on September 1, 2021 |
| Invoice 4 of | 10 | — | $92,322 | on October 1, 2021 |
| Invoice 5 of | 10 | — | $92,322 | on November 1, 2021 |
| Invoice 6 of | 10 | — | $92,322 | on December 1, 2021 |
| Invoice 7 of | 10 | — | $92,322 | on January 1, 2022 |
| Invoice 8 of | 10 | — | $92,322 | on February 1, 2022 |
| Invoice 9 of | 10 | — | $92,322 | on April 1, 2022 |
| Invoice 10 of | 10 | — | $92,322 | upon project completion |

The Fees and payment schedule above reflect a projected estimate agreed upon by the Parties. Should the Client wish to go beyond the projected estimate at any point in the project, Client and AREA 17 shall agree to execute an Amendment.

# Project Acceptance

AREA 17 shall not provide the Services until this SOW and its Master Agreement is fully executed and the Payment on Signature is received.

IN WITNESS WHEREOF, each party acknowledges that it has read and understood the terms of this SOW and agrees to be bound by such terms.

| Client name | | |
|---|---|---|
| Client name | | |
| Project name | Document version | Fees |
| Website Redesign | Client Version 1.0 | $TKTKTK |
| Client | AREA 17 | |
| Name: | Name: Mark Jarecke | |
| Title: | Title: Managing Director, New York | |
| Signature: | Signature: | |
| Date: | Date: | |
| Client billing contact (if different than MSA) | | |
| Name: | Email: | |
| Title | Phone: | |
