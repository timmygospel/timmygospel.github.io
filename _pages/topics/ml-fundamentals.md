---
permalink: /topics/ml-fundamentals/
title: "ML Fundamentals"
layout: single
author_profile: false
---

**Machine learning fundamentals** are the concepts that underpin every algorithm, every model, and every deployment decision. Understanding them deeply is what separates someone who can run a model from someone who can diagnose why it is failing and fix it.

This topic covers the core building blocks: how models learn, the sources of prediction error, and the different learning paradigms.

---

## Articles in this topic

<div class="article-list">
{% assign topic_posts = site.posts | where_exp: "post", "post.tags contains 'fundamentals'" %}
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
- [Overfitting &amp; Regularisation](/topics/overfitting-regularisation/)
- [All Topics](/topics/)
