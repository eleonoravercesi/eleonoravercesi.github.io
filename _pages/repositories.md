---
layout: page
permalink: /repos/
title: Blog
description: Some posts and repositories that might be helpful
nav: true
nav_order: 5
---


#### Tutorials

<div class="list-group">
  <a href="{{ '/blog/2026/installing-concorde-cplex/' | relative_url }}" class="list-group-item list-group-item-action flex-column align-items-start">
    <div class="d-flex w-100 justify-content-between">
      <h5 class="mb-1">Install Concorde with CPLEX</h5>
      <small>April 2026</small>
    </div>
    <p class="mb-1">A step-by-step guide to building the Concorde TSP solver with IBM ILOG CPLEX on Ubuntu 20.04.</p>
  </a>
</div>

<p></p>
<p></p>

#### GitHub Repositories

{% if site.data.repositories.github_repos %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos %}
    {% include repository/repo.html repository=repo %}
  {% endfor %}
</div>
{% endif %}