---
layout: page
permalink: /publications/
title: Papers
description: 
years: [2026,2025,2024,2022, 2021, 2020]
nav: true
nav_order: 3
---
<!-- _pages/publications.md -->
<div class="publications">

<h2>Journal Articles</h2>
{% bibliography -f papers -q @article %}

<h2>Conference Papers</h2>
{% bibliography -f papers -q @inproceedings %}

<h2>Preprints</h2>
{% bibliography -f papers -q @misc %}

</div>
