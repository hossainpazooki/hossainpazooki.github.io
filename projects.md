---
layout: default
title: Projects
---

<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">

# Projects

The list below updates automatically from my public GitHub repositories.

<div class="card-grid">
{% assign repos = site.github.public_repositories | where_exp: "r", "r.fork == false" | sort: "stargazers_count" | reverse %}
{% for repo in repos %}
  <div class="card">
    <h3><a href="{{ repo.html_url }}">{{ repo.name }}</a></h3>
    <p>{{ repo.description }}</p>
    <p class="small">⭐ {{ repo.stargazers_count }} • {{ repo.language }} • Updated {{ repo.pushed_at | date_to_string }}</p>
  </div>
{% endfor %}
</div>
