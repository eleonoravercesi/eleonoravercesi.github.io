---
layout: page
permalink: /repos/
title: Blog
description: Some posts and repositories that might be helpful
nav: true
nav_order: 5
---

#### Tutorials
In progress...

#### GitHub Repositories

{% if site.data.repositories.github_repos %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos %}
    {% include repository/repo.html repository=repo %}
  {% endfor %}
</div>
{% endif %}