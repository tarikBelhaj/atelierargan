---
layout: default
title: Blog
---

<h1>Nos articles</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%d %B %Y" }}</a>
    </li>
  {% endfor %}
</ul>
