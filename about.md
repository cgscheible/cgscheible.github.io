---
layout: page
title: About
permalink: /about/
---

Some posts on this blog:

[2023-11-05 Platform Engineering Maturity Modell]({% post_url 2023-11-05-Platform-Engineering-Maturity-Model %})


Tags:
{% for tag in site.tags %}
  <p>{{ tag[0] }}</p>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}


[jekyll-organization]: https://github.com/jekyll
