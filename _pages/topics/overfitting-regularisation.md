---
permalink: /topics/overfitting-regularisation/
title: "Overfitting & Regularisation"
layout: single
author_profile: false
---

**Overfitting** is one of the most common failure modes in machine learning. A model that overfits has memorised its training data rather than learned the underlying patterns — it looks impressive on known data and fails on anything new.

**Regularisation** is the family of techniques that constrain a model's complexity to prevent this. Understanding both — and knowing which fix to apply in which situation — is essential for building models that work in production.

---

## Articles in this topic

<div class="article-list">
{% assign topic_posts = site.posts | where_exp: "post", "post.tags contains 'overfitting'" %}
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

- [Model Evaluation](/topics/model-evaluation/)
- [ML Fundamentals](/topics/ml-fundamentals/)
- [All Topics](/topics/)
