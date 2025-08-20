---
layout: default
title: "Argan Atelier - Blog beauté huile d'argan"
description: "Découvrez tous les secrets de l'huile d'argan : bienfaits, routines beauté, conseils d'achat et comparatifs d'experts."
---

# Argan Atelier
## Beauté & bienfaits — l'huile d'argan, en profondeur

<div class="intro-section">
  <p>Bienvenue sur Argan Atelier, votre référence pour tout savoir sur l'huile d'argan. Découvrez nos articles, guides et conseils d'experts pour révéler la beauté naturelle de votre peau et de vos cheveux.</p>
</div>

---

## Articles récents

{% assign posts_to_show = site.posts | default: site.posts %}

{% if posts_to_show.size > 0 %}
  <div class="posts-list">
    {% for post in posts_to_show %}
      <article class="post-preview">
        <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
        <p class="post-meta">
          <time datetime="{{ post.date | date_to_xmlschema }}">
            {{ post.date | date: "%d %B %Y" }}
          </time>
          {% if post.author %} • Par {{ post.author }}{% endif %}
        </p>
        {% if post.excerpt %}
          <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
        {% endif %}
        <a href="{{ post.url | relative_url }}" class="read-more">Lire la suite →</a>
      </article>
    {% endfor %}
  </div>

  <!-- Navigation pagination (seulement si paginator existe) -->
  {% if paginator and paginator.total_pages > 1 %}
    <nav class="pagination" aria-label="Navigation des pages">
      {% if paginator.previous_page %}
        <a href="{{ paginator.previous_page_path | relative_url }}" class="pagination-link">
          ← Articles plus récents
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
    <p>Les premiers articles arrivent bientôt ! 🌟</p>
    <p>En attendant, découvrez <a href="/a-propos/">notre mission</a> ou <a href="/contact/">contactez-nous</a>.</p>
  </div>
{% endif %}