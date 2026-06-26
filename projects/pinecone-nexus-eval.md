---
type: project
title: Pinecone Nexus Evaluation
description: AREA 17's evaluation of Pinecone's Nexus (knowledge artifacts + NoQL) for an internal knowledge base and client RAG use cases.
tags:
  - project
  - area-17
---
# Pinecone Nexus Evaluation

[AREA 17](/clients/area-17/overview.md)'s evaluation of **Nexus**, [Pinecone](/clients/pinecone/overview.md)'s structured-retrieval product, for both an internal knowledge base and client-facing RAG use cases. The demo (June 23) ran with Jasmine (Head of Product, Nexus), Lucas Angstrom, and Aaron from Pinecone.

## Status

Evaluation in progress; a dedicated test environment and preview key to be configured.

## What Nexus is

Nexus addresses the failure modes of standard RAG (looping on chunks without understanding the underlying document) and context-window stuffing (slow, inaccurate, no source traceability). It compiles raw data into structured **"knowledge artifacts"** via a Curate runtime (ingest + design manifest), then queries them with **NoQL** — a declarative query language letting agents specify output shape, grounding, budget, and scope. Pinecone benchmarks it at ~94% higher accuracy than simple RAG on Gong transcripts, with lower token use and latency, and claims ~90% token-cost savings. It is API/endpoint-first; guardrails and prompts live in the consuming agent layer. See [RAG 2.0 / Structured Knowledge Retrieval](/concepts/rag-structured-retrieval.md).

## Use cases under consideration

- **Internal knowledge base** — AREA 17 IP is scattered across Slack, Figma decks, Drive, and BD responses; goal is an agnostic dataset of Markdown files that can be pointed at Nexus, Dobbin, or other tools. Figma export is a friction point (image-rich decks lose context as MD).
- **[Jane Street](/clients/jane-street/overview.md) personalization** — first-party data (LinkedIn source, user profile) + site content driving adaptive UI prompts for a recruitment funnel; the current RAG approach is MVP-level. Jasmine flagged that real-time site personalization may be better served by a vector DB directly.
- **[Pentagram](/clients/pentagram/overview.md) archive search** — an existing production RAG that is token-heavy; a candidate for a Nexus upgrade.
- **Website-as-dataset** — CMS pages rendered as Markdown (e.g. a `/md` route) ingested directly into Nexus.

## Key decision

**Ruled out [Snowflake](/clients/snowflake/overview.md)** for AREA 17's needs (per a June 25 note) while **continuing to evaluate [Pliable](/clients/pliable/overview.md) and Pinecone Nexus** for the agency's analytics/RAG direction.

## Next steps

- James to write up 1–2 use cases with identified datasets so Jasmine can configure a dedicated test environment and preview key.
- Lucas to set up a follow-up call and Slack channel.

## People

- [James Gillispie](/people/james-gillispie.md) — driving the evaluation; to define the test use cases.
- [Jasmine](/people/jasmine.md) — Head of Product for Nexus at Pinecone; provisioning the preview environment.

## Organization

[Pinecone](/clients/pinecone/overview.md)
