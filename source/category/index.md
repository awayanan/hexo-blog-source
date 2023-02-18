---
layout: page
permalink: /category/
---

<h1>Archive of posts from {{ page.date | date: "%B %Y" }}</h1>

<ul class="posts">
{% for post in page.posts %}
  <li>
    <a class="post-link" href="{{ post.url | relative_url }}">{{ post.categories }}</a>
  </li>
{% endfor %}
</ul>