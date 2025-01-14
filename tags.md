---
layout: page
title: Tags
permalink: /tags/
---

{% for tag in site.tags %}
  <h3 id="{{ tag[0] }}">{{ tag[0] }}</h3>
  <ul class="post-list">
    {% for post in tag[1] %}
      <li>
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
        <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
      </li>
    {% endfor %}
  </ul>
{% endfor %}

