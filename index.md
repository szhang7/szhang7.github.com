---
layout: page
title: Index
header: Posts By Index
group: navigation
---
{% include JB/setup %}

<h2>Recent Posts</h2>
<ul class="posts">
  {% for post in site.posts limit:10 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

