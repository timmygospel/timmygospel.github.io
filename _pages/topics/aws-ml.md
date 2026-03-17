---
permalink: /topics/aws-ml/
title: "AWS & SageMaker"
layout: single
author_profile: false
---

**AWS provides a comprehensive ML stack** built around Amazon SageMaker — a fully managed service that covers every stage of the ML workflow from data preparation through training, evaluation, and deployment.

This topic covers the AWS services most relevant to machine learning practitioners and the AWS ML Specialty exam.

---

## Articles in this topic

<div class="article-list">
{% assign topic_posts = site.posts | where_exp: "post", "post.tags contains 'aws-sagemaker' or post.categories contains 'aws'" %}
{% if topic_posts.size > 0 %}
  {% for post in topic_posts %}
  <div class="article-list__item">
    <div class="article-list__meta">{{ post.date | date: "%B %d, %Y" }}</div>
    <h2 class="article-list__title"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <p class="article-list__excerpt">{{ post.excerpt | strip_html | truncate: 160 }}</p>
  </div>
  {% endfor %}
{% else %}
  <p>Articles coming soon. Every ML article on this site includes an AWS section connecting the concept to SageMaker and the broader AWS stack.</p>
{% endif %}
</div>

---

## Related topics

- [ML Fundamentals](/topics/ml-fundamentals/)
- [Model Evaluation](/topics/model-evaluation/)
- [All Topics](/topics/)
