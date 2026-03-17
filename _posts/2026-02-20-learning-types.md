---
title: "Supervised, Unsupervised, and Reinforcement Learning: What's the Difference?"
date: 2026-02-20
categories: [machine-learning]
tags: [fundamentals, supervised-learning, unsupervised-learning, reinforcement-learning]
excerpt: "Supervised, unsupervised, and reinforcement learning are the three core paradigms of machine learning. Each answers a different type of question and requires a different type of data."
layout: single
author_profile: true
read_time: true
toc: true
toc_label: "In this article"
faqs:
  - q: "What is the difference between supervised and unsupervised learning?"
    a: "Supervised learning trains on labelled data — each example has an input and a known correct output. The model learns to predict that output for new inputs. Unsupervised learning trains on unlabelled data and discovers patterns, structure, or groupings without any target variable."
  - q: "What is supervised learning?"
    a: "Supervised learning is a type of machine learning where a model is trained on labelled examples — pairs of inputs and known correct outputs. The model learns a mapping from inputs to outputs and uses that mapping to make predictions on new, unseen inputs. Common tasks include classification and regression."
  - q: "What is unsupervised learning?"
    a: "Unsupervised learning is a type of machine learning that works without labels. The model discovers patterns, groupings, or structure that exists in the data on its own. Common tasks include clustering, dimensionality reduction, and association rule mining."
  - q: "What is reinforcement learning?"
    a: "Reinforcement learning is a type of machine learning where an agent learns by interacting with an environment. The agent takes actions, receives rewards or penalties, and gradually learns a policy that maximises cumulative reward. It is used in robotics, game playing, and recommendation optimisation."
  - q: "When should I use supervised vs unsupervised learning?"
    a: "Use supervised learning when you have labelled data and want to predict a specific output — classification or regression. Use unsupervised learning when you have no labels and want to discover patterns in the data — clustering, anomaly detection, or dimensionality reduction."
  - q: "What AWS services support each type of learning?"
    a: "For supervised learning: SageMaker XGBoost, Linear Learner, and Image Classification. For unsupervised learning: SageMaker K-Means (clustering), PCA (dimensionality reduction), and Random Cut Forest (anomaly detection). For reinforcement learning: SageMaker RL with Ray RLlib, and AWS DeepRacer for hands-on practice."
---

**Supervised**, **unsupervised**, and **reinforcement learning** are the three core paradigms of machine learning — each one answers a different type of question and requires a fundamentally different type of data.

{% capture def %}
**Supervised learning** learns from labelled data to predict an output. **Unsupervised learning** finds patterns in unlabelled data without any target variable. **Reinforcement learning** learns through trial and error by receiving rewards and penalties for actions taken in an environment. Choosing the right paradigm starts with the question: what data do I have, and what do I want to discover?
{% endcapture %}
{% include callout.html type="definition" label="Definition" content=def %}

## Supervised Learning

Supervised learning trains on **labelled data** — a dataset where every example has both an input and a known correct output.

The model learns a mapping from inputs to outputs during training, then applies that mapping to predict outputs for new, unseen inputs.

### The Two Tasks

**Classification** — predict a discrete category.
> Input: email text → Output: spam or not spam
> Input: medical scan → Output: benign or malignant

**Regression** — predict a continuous numerical value.
> Input: house features → Output: sale price
> Input: historical sales → Output: next month's demand

### When to Use It

Use supervised learning when:
- You have labelled examples of the outcome you want to predict
- You want to predict a specific target variable for new inputs
- The task can be framed as "given X, what is Y?"

### AWS Supervised Learning

- **SageMaker XGBoost** — gradient boosted trees for tabular classification and regression
- **SageMaker Linear Learner** — fast linear/logistic regression, optimisable for precision or recall
- **SageMaker Image Classification** — CNN-based image labelling
- **Amazon Comprehend** — supervised NLP for sentiment, entities, and custom classification

## Unsupervised Learning

Unsupervised learning works with **unlabelled data** — no target variable, no correct answers. The algorithm finds structure that already exists in the data.

### The Three Main Tasks

**Clustering** — group similar examples together without predefined categories.
> Input: customer transaction histories → Output: customer segments

**Dimensionality reduction** — compress high-dimensional data into fewer dimensions while preserving structure.
> Input: 1,000 raw features → Output: 10 meaningful components

**Association rule mining** — find items that frequently co-occur.
> Input: supermarket baskets → Output: "customers who buy X also buy Y"

{% capture exam_tip %}
The AWS ML exam commonly asks you to match a business scenario to the correct learning type. The deciding factor is almost always the data: if labels exist and you are predicting a target, it is supervised. If there are no labels and you are discovering structure, it is unsupervised. If an agent is learning through interaction with an environment, it is reinforcement.
{% endcapture %}
{% include callout.html type="exam" label="Exam Tip" content=exam_tip %}

### When to Use It

Use unsupervised learning when:
- You have no labels and labelling would be expensive or impractical
- You want to explore and understand the structure of your data
- The task is discovery, not prediction — segmentation, anomaly detection, pattern finding

### AWS Unsupervised Learning

- **SageMaker K-Means** — clustering algorithm for customer segmentation and grouping
- **SageMaker PCA** — principal component analysis for dimensionality reduction
- **SageMaker Random Cut Forest** — anomaly detection in time series and tabular data
- **Amazon Personalize** — co-occurrence-based recommendation (association-style patterns at scale)

## Reinforcement Learning

Reinforcement learning is fundamentally different from both. There is no fixed dataset — instead, an **agent** learns by interacting with an **environment**.

At each step:
1. The agent observes the current state of the environment
2. The agent takes an action
3. The environment returns a reward (positive or negative)
4. The agent updates its policy to maximise future cumulative reward

Over many iterations, the agent learns a **policy** — a strategy for choosing actions in any given state.

### When to Use It

Use reinforcement learning when:
- The task involves sequential decision-making
- The correct action in each situation is not known in advance — only the reward signal
- The system can be modelled as an agent interacting with an environment

Common use cases: robotics, game-playing AI, recommendation system optimisation, autonomous vehicle control, resource scheduling.

### AWS Reinforcement Learning

- **SageMaker RL** — managed RL training using Ray RLlib and popular simulation environments
- **AWS DeepRacer** — a physical/virtual racing car used to learn RL concepts hands-on through a competitive league
- **AWS DeepComposer** — applies generative ML and RL concepts to music composition

{% capture tip %}
**Quick comparison:**

| | Supervised | Unsupervised | Reinforcement |
|---|---|---|---|
| Data | Labelled | Unlabelled | Environment + rewards |
| Goal | Predict a target | Discover structure | Maximise cumulative reward |
| Examples | Classification, regression | Clustering, PCA, association | Robotics, games, recommendations |
| AWS | XGBoost, Linear Learner | K-Means, PCA, RCF | SageMaker RL, DeepRacer |
{% endcapture %}
{% include callout.html type="tip" label="Comparison Table" content=tip %}

## Beyond the Three: Semi-Supervised and Self-Supervised

**Semi-supervised learning** uses a small amount of labelled data alongside a large amount of unlabelled data. The model uses the labelled examples as anchors and the unlabelled examples to learn better representations. Useful when labelling is expensive — medical imaging is a classic example.

**Self-supervised learning** is how modern large language models are trained. The model generates its own labels from the structure of the data — for example, by masking a word and training the model to predict it from context. No human-labelled data is required at pre-training time.

{% capture warning %}
A common mistake is assuming that more data automatically means supervised learning is possible. Labelled data and raw data are not the same thing. A dataset of one billion unlabelled images cannot be used for supervised image classification without first labelling examples. The availability of labels — not the volume of data — determines whether supervised learning is viable.
{% endcapture %}
{% include callout.html type="warning" label="Common Mistake" content=warning %}

{% include key-takeaways.html items="Supervised learning trains on labelled data to predict a target — used for classification and regression.|Unsupervised learning finds patterns in unlabelled data — used for clustering, dimensionality reduction, and association.|Reinforcement learning trains an agent through interaction with an environment, guided by a reward signal — used for sequential decision-making.|Choose based on your data: labels → supervised; no labels → unsupervised; environment + reward → reinforcement.|AWS supports all three: XGBoost and Linear Learner for supervised; K-Means, PCA, and Random Cut Forest for unsupervised; SageMaker RL and DeepRacer for reinforcement.|Semi-supervised and self-supervised learning extend these paradigms — self-supervised is how large language models are pre-trained." %}

{% include related-posts.html %}
{% include faq.html %}
{% include article-schema.html %}
