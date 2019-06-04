---
layout: default
---

# Posts
  {% for post in site.posts %}
    {% if post.categories contains 'blog' %}
    <section class="post">
    ## <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a> (<small>{{post.date | date: "%y-%m-/%d/" }}</small>
    {{ post.description }}
    </section>
    {% endif %}
  {% endfor %}
