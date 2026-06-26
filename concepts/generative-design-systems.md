---
type: concept
title: Generative / Data-Driven Design Systems
description: Using emergence mathematics to generate an ownable visual identity, driven by a CMS controller and interaction layer.
tags:
  - concept
  - theme
---
# Generative / Data-Driven Design Systems

A recurring approach to brand and web identity that uses **emergence mathematics** — Wolfram rules, cellular automata, reaction-diffusion, Turing/Voronoi patterns — to generate an ownable visual system rather than hand-drawing static assets. The system is driven by a CMS controller (page / component / global level) and brought to life with interaction (cursor-trail / unmasking), bridging design and engineering through vibe-coded prototypes.

## The idea

Instead of a fixed logo-and-palette identity, the brand becomes a *generative system*: a small set of rules produces an emergent pattern, and the rules themselves (proximity, position, shape, color) become the brand's expressive controls. The same engine can drive header canvas animations, user-facing controls, and thumbnail generation for cards that lack imagery.

## Why it recurs

It resonates with technically-minded clients who want conceptual rationale behind visuals (Jane Street's stakeholders are ML / Ivy-League), and it answers the broader shift toward *dynamic* design systems in an AI-disrupted landscape — where psychographics matter more than demographics and the identity needs to feel alive, not templated. Rapid prototyping (a Next.js app-router tool, hand-coded canvas) lets the team convert ideation into shareable explorations fast.

## Concrete examples

- **[Jane Street Website Redesign](/projects/jane-street-redesign.md)** — the origin of the approach. [Miguel](/people/miguel.md) and the team built a canvas tool generating animated textures and thumbnails from cellular automata / Wolfram rule sets. Key learnings from pattern exploration: a reduced palette (monochromatic + grays) dramatically improved the feel; a dotted-grid "layer" (blank canvas → dot grid → emergent pattern) with a cursor-trail unmasking interaction reads better than constant full-screen exposure; dark mode is a priority test; and the most boring/redundant rules should be culled, keeping only the graphically interesting ones.
- **[Truth Initiative Pitch](/projects/truth-initiative-pitch.md)** — the "dynamic design systems" framing and the Wolfram-rules direction carried into the pitch's reframed opportunity narrative.

## Tensions

Performance matters at scale (an emergent pattern can draw a million dots), so these systems tend to live as background texture and hero treatments rather than everywhere. There is also the standing risk that conceptual ambition outpaces functional delivery — "a website has to function as a website."
