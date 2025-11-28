---
layout: default
title: Home
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

<section class="hero">
  <h1>Hi, I'm Hossain Pazooki</h1>
  <p class="small">I build systems at the edge of networking, data science, and fintech.</p>
  <p>
    <strong>Featured:</strong> <a href="{{ '/rwa' | relative_url }}">RWA Compliance Navigator</a>
    <span class="badge">New</span>
  </p>
</section>

## Latest public repositories
<div class="card-grid">
{% assign repos = site.github.public_repositories | where_exp: "r", "r.fork == false" | sort: "pushed_at" | reverse %}
{% for repo in repos limit: 6 %}
  <div class="card">
    <h3><a href="{{ repo.html_url }}">{{ repo.name }}</a></h3>
    <p>{{ repo.description }}</p>
    <p class="small">{{ repo.language }} • Updated {{ repo.pushed_at | date_to_string }}</p>
  </div>
{% endfor %}
</div>

<p class="footer"><a href="{{ '/projects' | relative_url }}">See all projects →</a></p>
