---
layout: default
title: Blog
permalink: /blog
---

<h2>Articles récents</h2>
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a> — {% include date_fr.html date=post.date %}
    </li>
  {% endfor %}
</ul>
