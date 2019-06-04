---
title: Jimmy Mattsson
layout: default
---

<section class="posts">
  {% for post in site.posts %}
    {% if post.categories contains 'blog' %}     
    <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></small>
    <p><span class="date">{{post.date | date: "%y-%m-%d" }}</span> {{ post.description }}</p>
    {% endif %}
  {% endfor %}
</section>
