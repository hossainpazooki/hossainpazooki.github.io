---
layout: default
title: Home
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

<div class="profile-card">
  <img
    class="profile-avatar"
    src="/assets/img/hossain.jpeg"
    alt="Hossain Pazooki"
  >

  <div class="profile-links">
    <!-- Add more links (LinkedIn, email) here when you’re ready -->
    <a class="icon-link" href="https://github.com/hossainpazooki" aria-label="GitHub profile">
      <span class="icon-link-text">GH</span>
    </a>
  </div>

  <h1 class="profile-name">Hossain Pazooki</h1>

  <p class="profile-intro">
    I build systems at the edge of networking, data science, and fintech, and I like turning complex rules into
    executable models, workflow tools, and clear, audit‑ready documentation.
  </p>

  <div class="pill-nav">
    <a href="#projects" class="pill">Projects</a>
    <a href="#about" class="pill">About</a>
    <a href="#skills" class="pill">Skills</a>
    <a href="{{ '/rwa' | relative_url }}" class="pill">RWA Navigator</a>
  </div>
</div>

## Projects / Technical Portfolio {#projects}

- **Financial Regulation Document Analyzer (RAG):** Q&A over regulatory PDFs using embeddings; returns sourced excerpts. Added explicit rule stubs and tests to demonstrate traceable, executable logic alongside retrieval.
- **PrecisionFDA Multi‑omics Pipeline:** Three‑step process—data cleanse/context → Spark Random Forest (HPO) → correlation clustering to sanity‑check dimensionality → XGBoost for sparse outcomes.
- **Econometrics Time‑Series (USC):** STATA models with specification, diagnostics, and clear documentation.
- **High‑Throughput UDP File Transfer:** Custom protocol design; reliability/throughput trade‑offs; simple test harness.

## About {#about}

Combine research rigor, fast learning, and reliable execution to turn complex rules into executable models, prototype workflow tools, and write clear, audit‑ready docs.

## Skills {#skills}

Rule Modeling · Decision Tables · Exception/Precedence Policies · Algorithmic Thinking · Python · SQL · C++ · Git · Information Retrieval · A/B Testing · Time‑Series · Spark · XGBoost · Documentation · Change Management · Process Mapping

---

## More on GitHub

<div class="card-grid">
{% assign repos = site.github.public_repositories
   | where_exp: "r", "r.fork == false"
   | sort: "pushed_at"
   | reverse %}
{% for repo in repos limit: 6 %}
  {% if repo.name != "hossainpazooki.github.io" and repo.name != "RWAs" and repo.name != "TCP-IP" %}
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

<p class="footer"><a href="{{ '/projects' | relative_url }}">See all repositories →</a></p>
