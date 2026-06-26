---
type: organization
title: Pinecone
description: Vector-DB vendor pitching Nexus, a structured knowledge-retrieval runtime.
tags:
  - client
  - pinecone
---
# Pinecone

Pinecone is a vector-database vendor pitching **Nexus**, a curation runtime that compiles raw data into structured "knowledge artifacts" queried via a query language (NoQL). The pitch claims roughly 90-94% token savings and higher accuracy than naive RAG by retrieving from structured artifacts rather than embedding-and-similarity over raw chunks.

## Why it matters

Nexus was evaluated for both internal knowledge-base use and client-facing applications. Two concrete use cases surfaced: personalization for the [Jane Street Website Redesign](/projects/jane-street-redesign.md) (first-party data + site content) and a RAG layer over the Pentagram archive. The evaluation is captured in the [Pinecone Nexus Evaluation](/projects/pinecone-nexus-eval.md).

Nexus sits inside the broader [RAG 2.0 / structured knowledge retrieval](/concepts/rag-structured-retrieval.md) theme — the shift from chunk-and-embed RAG toward compiled, structured, queryable knowledge.

## Key people

- [Jasmine](/people/jasmine.md)

## Related

- Project: [Pinecone Nexus Evaluation](/projects/pinecone-nexus-eval.md)
- Concept: [RAG 2.0 / Structured Knowledge Retrieval](/concepts/rag-structured-retrieval.md)
