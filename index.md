---
layout: default
title: Home
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

<section class="hero">
  <div class="hero-inner">
    <div class="hero-text">
      <h1>Hi, I'm Hossain Pazooki</h1>
      <p class="small">
        I build systems at the edge of networking, data science, and fintech.
      </p>
      <p>
        <strong>Featured:</strong>
        <a href="{{ '/rwa' | relative_url }}">RWA Compliance Navigator</a>
        <span class="badge">New</span>
      </p>
    </div>
    <div class="hero-photo">
      <img
        class="avatar"
        src="/assets/img/hossain.jpeg"
        alt="Hossain Pazooki"
      >
    </div>
  </div>
</section>

## About

### Summary
Combine research rigor, fast learning, and reliable execution to turn complex rules into executable models, prototype workflow tools, and write clear, audit‑ready docs.

## Projects / Technical Portfolio

- **Financial Regulation Document Analyzer (RAG):** Q&A over regulatory PDFs using embeddings; returns sourced excerpts. Added explicit rule stubs and tests to demonstrate traceable, executable logic alongside retrieval.
- **PrecisionFDA Multi‑omics Pipeline:** Three‑step process—data cleanse/context → Spark Random Forest (HPO) → correlation clustering to sanity‑check dimensionality → XGBoost for sparse outcomes.
- **Econometrics Time‑Series (USC):** STATA models with specification, diagnostics, and clear documentation.
- **High‑Throughput UDP File Transfer:** Custom protocol design; reliability/throughput trade‑offs; simple test harness.

## Skills

Rule Modeling · Decision Tables · Exception/Precedence Policies · Algorithmic Thinking · Python · SQL · C/C++ · Git · Information Retrieval · A/B Testing · Time‑Series · Spark · XGBoost · Documentation · Change Management · Process Mapping

## Latest public repositories
<div class="card-grid">
{% assign repos = site.github.public_repositories | where_exp: "r", "r.fork == false" | sort: "pushed_at" | reverse %}
{% for repo in repos limit: 6 %}
  {% if repo.name != "hossainpazooki.github.io" %}
    <div class="card">
      <h3><a href="{{ repo.html_url }}">{{ repo.name }}</a></h3>
      <p>{{ repo.description }}</p>
      <p class="small">
        {{ repo.language }} • Updated {{ repo.pushed_at | date_to_string }}
      </p>
    </div>
  {% endif %}
{% endfor %}

</div>

<p class="footer"><a href="{{ '/projects' | relative_url }}">See all projects →</a></p>
