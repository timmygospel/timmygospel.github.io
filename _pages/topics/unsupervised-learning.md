---
permalink: /topics/unsupervised-learning/
title: "Unsupervised Learning"
layout: single
author_profile: false
---

**Unsupervised learning** is the branch of machine learning that works without labels. Instead of learning to predict a target, unsupervised algorithms discover structure that already exists in the data — clusters, patterns, associations, and compressed representations.

It is used wherever labelled data is unavailable, expensive, or simply unnecessary — customer segmentation, anomaly detection, recommendation systems, and exploratory data analysis.

---

## Articles in this topic

<div class="article-list">
{% assign topic_posts = site.posts | where_exp: "post", "post.tags contains 'unsupervised-learning'" %}
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
- [Feature Engineering](/topics/feature-engineering/)
- [All Topics](/topics/)
