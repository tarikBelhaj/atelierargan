---
layout: default
title: "Tous nos articles"
permalink: /articles/
description: "Découvrez tous nos articles de blog"
---

# 📝 Tous nos articles

{% if site.posts == empty %}
  <p>Aucun article pour le moment.</p>
{% else %}

<ul class="articles-list">
  {% assign posts_all = site.posts | sort: "date" | reverse %}
  {% for post in posts_all %}
    <li class="article-item">
      <a href="{{ post.url | relative_url }}"><strong>{{ post.title }}</strong></a><br>
      <small>Publié le {{ post.date | date: "%d %B %Y" }}</small><br>
      <p>{{ post.description | default: post.excerpt | strip_html | truncatewords: 20 }}</p>
    </li>
  {% endfor %}
</ul>

<hr>

<div class="pagination-links">
  <p><strong>{{ site.posts.size }}</strong> articles au total</p>
  <p>Navigation par pages :
    {% assign per_page = site.paginate | default: 6 %}
    {% assign total_pages = site.posts.size | divided_by: per_page %}
    {% if site.posts.size modulo per_page > 0 %}
      {% assign total_pages = total_pages | plus: 1 %}
    {% endif %}
    {% for i in (1..total_pages) %}
      {% if i == 1 %}
        <a href="{{ '/' | relative_url }}">Page {{ i }}</a>
      {% else %}
        <a href="{{ '/page' | append: i | append: '/' | relative_url }}">Page {{ i }}</a>
      {% endif %}
      {% unless forloop.last %} • {% endunless %}
    {% endfor %}
  </p>
</div>

{% endif %}