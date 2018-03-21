---
layout: default
title: Blog
permalink: /blog
---

<div class="section typeset">
  <div class="single-measure">
    {% if site.posts == empty %}
      <h2>There's currently no posts to display!</h1>
    {% endif %}
    {% for post in site.posts %}
      <h2><a class="post-title" href="/{{ post.permalink }}">{{ post.title }}</a></h2>
      <p class="caption">{{ post.date | date: "%B %d, %Y" }}</p>
      <p>{{ post.excerpt | remove: '<p>' | remove: '</p>' }}</p>
      <p><a href="/{{ post.permalink }}">Read more</a></p>
    {% endfor %}
  </div>
</div>