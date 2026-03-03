---
layout: page
permalink: /publications/
title: Publications
description: A comprehensive list of my research publications
nav: true
nav_order: 1
---

<!-- _pages/publications.md -->
<div class="publications">

{% comment %}
Group publications by year in descending order
{% endcomment %}

{% assign years = "" | split: "" %}
{% for entry in site.bibliography_list %}
  {% unless years contains entry.year %}
    {% assign years = years | push: entry.year %}
  {% endunless %}
{% endfor %}

{% assign sorted_years = years | sort | reverse %}

{% for year in sorted_years %}
  <div class="year-section">
    <h3 class="year-header">{{ year }}</h3>
    {% bibliography -f {{ site.scholar.bibliography }} -q @*[year={{ year }}]* %}
  </div>
{% endfor %}

</div>