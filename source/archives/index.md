---
layout: page
permalink: /archives.html
---

<h2>Archives</h2>
<ul>
  {% for post in site.posts %}

    {% unless post.next %}
      <h3>{{ post.date | date: '%B %Y' }}</h3>
    {% else %}
      {% capture year %}{{ post.date | date: '%b %-d, %Y' }}{% endcapture %}
      {% capture nyear %}{{ post.next.date | date: '%b %-d, %Y' }}{% endcapture %}
      {% if year != nyear %}
        <h3>{{ post.date | date: '%B %Y' }}</h3>
      {% endif %}
    {% endunless %}

    <li>{{ post.date | date:"%b" }} <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
