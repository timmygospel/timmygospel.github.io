---
permalink: /topics/feature-engineering/
title: "Feature Engineering"
layout: single
author_profile: false
---

**Feature engineering** is the process of transforming raw data into input features that help machine learning models learn effectively. It is often where the most practical model improvement happens — better features consistently outperform more complex algorithms on the same data.

This topic covers encoding, scaling, feature creation, feature selection, and handling missing values.

---

## Articles in this topic

<div class="article-list">
{% assign topic_posts = site.posts | where_exp: "post", "post.tags contains 'feature-engineering'" %}
{% if topic_posts.size > 0 %}
  {% for post in topic_posts %}
  <div class="article-list__item">
    <div class="article-list__meta">{{ post.date | date: "%B %d, %Y" }}</div>
    <h2 class="article-list__title"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <p class="article-list__excerpt">{{ post.excerpt | strip_html | truncate: 160 }}</p>
  </div>
  {% endfor %}
{% else %}
  <p>Articles coming soon.</p>
{% endif %}
</div>

---

## Related topics

- [ML Fundamentals](/topics/ml-fundamentals/)
- [Unsupervised Learning](/topics/unsupervised-learning/)
- [All Topics](/topics/)
