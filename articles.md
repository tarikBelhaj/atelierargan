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

<div class="articles-grid">
  {% assign posts_all = site.posts | sort: "date" | reverse %}
  {% for post in posts_all %}
    <article class="article-card">
      <a class="article-thumb" href="{{ post.url | relative_url }}">
        {% if post.image %}
          <img src="{{ post.image | relative_url }}" alt="{{ post.image_alt | default: post.title }}">
        {% else %}
          <div class="thumb-placeholder" aria-hidden="true">ARGAN</div>
        {% endif %}
      </a>

      <div class="article-body">
        <h2 class="article-title">
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </h2>

        <p class="article-meta">
          <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%d %B %Y" }}</time>
          {% if post.author %} • {{ post.author }}{% endif %}
        </p>

        <p class="article-excerpt">
          {{ post.description | default: post.excerpt | strip_html | truncatewords: 28 }}
        </p>

        <a class="article-read" href="{{ post.url | relative_url }}">Lire la suite →</a>
      </div>
    </article>
  {% endfor %}
</div>

<hr class="articles-sep">

<div class="pagination-links">
  <p><strong>{{ site.posts.size }}</strong> articles au total</p>
  <p>Navigation par pages :
    {% assign per_page = site.paginate | default: 6 %}
    {% assign total_pages = site.posts.size | divided_by: per_page %}
    {% assign remainder = site.posts.size | modulo: per_page %}
    {% if remainder > 0 %}
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