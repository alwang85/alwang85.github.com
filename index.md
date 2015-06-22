---
layout: page
title: Welcome to Alex Wang's tech blog!
---
{% include JB/setup %}

Here are some of my recent posts while I dive deeper into the MEAN stack and good coding practices.

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



