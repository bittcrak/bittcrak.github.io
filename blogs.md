---
layout: default
title: Blogs
---

# Blogs

<ul>
{% for post in site.pages %}
  {% if post.path contains 'blogs/' and post.path contains '.md' %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <small>{{ post.date | date: "%-d %B %Y" }}</small>
  </li>
  {% endif %}
{% endfor %}
</ul>

