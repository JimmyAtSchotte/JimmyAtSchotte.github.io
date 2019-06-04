---
title: Jimmy Mattsson
layout: default
---

<section class="posts">
  {% for post in site.posts %}
    {% if post.categories contains 'blog' %}     
    <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
    <p><span class="date">{{post.date | date: "%y-%m-%d" }}</span> {{ post.ingress }}</p>
    {% endif %}
  {% endfor %}
</section>
