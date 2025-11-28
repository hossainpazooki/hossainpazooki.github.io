---
layout: default
title: RWA Compliance Navigator
permalink: /rwa
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

# RWA Compliance Navigator

A document-grounded Q&A tool for real‑world‑asset (RWA) compliance. It ingests regulatory PDFs/DOCX, builds a hybrid retrieval index (embeddings + BM25), and answers questions **only** from the uploaded sources, with section‑level citations.

## Highlights
- **Provision-aware ingestion:** detect Articles/Sections/§ and keep page spans
- **Hybrid retrieval:** vector + lexical with reranking
- **Strict grounding:** every claim cites *document • article/section • page*
- **Filters:** jurisdiction, pillar (venues/cash/collateral/global), instrument type, effective date
- **Compare mode:** side-by-side across versions/jurisdictions

## Stack (MVP)
- FastAPI, Chroma/pgvector, OpenAI (LLM + embeddings), optional OpenSearch for BM25
- Jekyll for this site; the app itself is a separate repo/service

## Links
- **Repo:** _coming soon_ (placeholder)
- **Demo:** _optional_

_If you're reviewing this page before the repo is public, ping me for access._
