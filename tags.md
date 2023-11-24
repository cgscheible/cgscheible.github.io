---
layout: page
title: Tags
permalink: /tags/
---

{% for tag in site.tags %}
  <p>{{ tag[0] }}</p>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}

