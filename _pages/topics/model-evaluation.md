---
permalink: /topics/model-evaluation/
title: "Model Evaluation"
layout: single
author_profile: false
---

**Model evaluation** is the practice of measuring whether a machine learning model is actually doing what you need it to do — not just on training data, but on data it has never seen.

Choosing the wrong metric can make a useless model look successful. Evaluating on training data alone guarantees overestimates of real-world performance. This topic covers the metrics, methods, and pitfalls of honest model evaluation.

---

## Articles in this topic

<div class="article-list">
{% assign topic_posts = site.posts | where_exp: "post", "post.tags contains 'model-evaluation'" %}
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

- [Overfitting &amp; Regularisation](/topics/overfitting-regularisation/)
- [ML Fundamentals](/topics/ml-fundamentals/)
- [All Topics](/topics/)
