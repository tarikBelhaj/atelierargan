
---
layout: default
title: "Tous nos articles"
permalink: /articles/
---

# 📝 Tous nos articles

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}"><strong>{{ post.title }}</strong></a><br>
      <small>Publié le {{ post.date | date: "%d %B %Y" }}</small><br>
      <p>{{ post.description }}</p>
    </li>
  {% endfor %}
</ul>