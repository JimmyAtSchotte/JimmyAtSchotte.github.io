---
title: Jimmy Mattsson
layout: default
---

<section class="posts">
  {% for post in site.posts %}
    {% if post.categories contains 'blog' %}     
    <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a> (<small>{{post.date | date: "%y-%m-%d" }}</small>
    <p>{{ post.description }}</p>
    {% endif %}
  {% endfor %}
</section>
