---
layout: page
title: Ongoing Projects
permalink: /projects/
description:
nav: true
nav_order: 4
horizontal: false
---

<style>
  .project-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 16px;
    align-items: stretch;      /* all cards in a row get the same height */
  }
  .project-grid > .grid-sizer {
    display: none !important;  /* Masonry helper, not needed in a CSS grid */
  }
  .project-grid > .grid-item {
    width: auto !important;    /* drop the theme's fixed width */
    position: static !important;
    float: none !important;
    margin: 0 !important;
  }
  .project-grid > .grid-item > a,
  .project-grid .card {
    display: block;
    height: 100%;
  }
</style>

<!-- pages/projects.md -->
<div class="projects">
{%- if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {%- for category in page.display_categories %}
  <h2 class="category">{{ category }}</h2>
  {%- assign categorized_projects = site.projects | where: "category", category -%}
  {%- assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="project-grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
  {% endfor %}

{%- else -%}
<!-- Display projects without categories -->
{%- assign sorted_projects = site.projects | sort: "importance" -%}
  <!-- Generate cards for each project -->
{% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="project-grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
{%- endif -%}
</div>