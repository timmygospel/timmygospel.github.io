---
permalink: /articles/
title: "All Articles"
layout: single
author_profile: false
---

<div class="article-list">
{% for post in site.posts %}
<div class="article-list__item">
  <div class="article-list__meta">{{ post.date | date: "%B %d, %Y" }} &middot; {{ post.read_time | default: "5" }} min read</div>
  <h2 class="article-list__title"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
  <p class="article-list__excerpt">{{ post.excerpt | strip_html | truncate: 180 }}</p>
  <div class="article-list__tags">
    {% for tag in post.tags %}
    <a href="/tag/{{ tag | slugify }}/" class="topic-pill">{{ tag }}</a>
    {% endfor %}
  </div>
</div>
{% endfor %}
</div>
