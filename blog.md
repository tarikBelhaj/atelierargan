---
layout: default
title: Blog
permalink: /blog/
paginate: true
---

# Articles récents

{% assign posts_to_show = paginator.posts | default: site.posts %}

{% if posts_to_show.size > 0 %}
  <div class="posts-list">
    {% for post in posts_to_show %}
      <article class="post-preview">
        <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
        <p class="post-meta">
          <time datetime="{{ post.date | date_to_xmlschema }}">
            {{ post.date | date: "%d %B %Y" }}
          </time>
        </p>
        {% if post.excerpt %}
          <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
        {% endif %}
      </article>
    {% endfor %}
  </div>

  <!-- Navigation pagination (seulement si paginator existe) -->
  {% if paginator %}
    <nav class="pagination" aria-label="Navigation des pages">
      {% if paginator.previous_page %}
        <a href="{{ paginator.previous_page_path | relative_url }}" class="pagination-link">
          ← Précédent
        </a>
      {% endif %}

      <span class="pagination-info">
        Page {{ paginator.page }} sur {{ paginator.total_pages }}
      </span>

      {% if paginator.next_page %}
        <a href="{{ paginator.next_page_path | relative_url }}" class="pagination-link">
          Suivant →
        </a>
      {% endif %}
    </nav>
  {% endif %}

{% else %}
  <div class="no-posts">
    <p>Aucun article pour le moment.</p>
    <p><a href="/">← Retour à l'accueil</a></p>
  </div>
{% endif %}