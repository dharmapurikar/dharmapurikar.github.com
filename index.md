---
layout: page
title: Home
---

<!-- Show last 10 posts here -->
{% for post in site.posts limit: 5  %}
  <p class="date">{{ post.date | date_to_string }}</p>
  <h3><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h3>
  {{ post.content }}
  <p> Tags - |
  {% for tag in post.tags %}
    <a href="#">{{ tag }}</a> |
  {% endfor %}
  </p>
  <hr/>
{% endfor %}
