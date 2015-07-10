---
layout: media
permalink: /portfolio/
title: "Portfolio"
comments: yes
---

## Portfolio

Here's a list of my projects sorted by recency:


<ul class="tags-box">
<div class="tiles">
{% assign projects = site.projects %}
{% for project in projects reversed %}
	{% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
</ul>