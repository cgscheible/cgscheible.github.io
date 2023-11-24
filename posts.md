---
layout: page
title: Posts
permalink: /posts/
---

{% for post in site.posts %}
  <ul>
    <li>
      <a href="{{ post.url }}">
        {{ post.title }}
      </a>
    </li>
  </ul>
{% endfor %}

