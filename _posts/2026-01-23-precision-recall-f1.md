---
title: "Precision, Recall, and F1 Score Explained: Choosing the Right Metric"
date: 2026-01-23
categories: [machine-learning]
tags: [model-evaluation, classification, metrics, fundamentals]
excerpt: "Precision, recall, and F1 score measure different things in a classification model. Knowing which one to optimise for — and why — is one of the most practical skills in machine learning."
layout: single
author_profile: true
read_time: true
toc: true
toc_label: "In this article"
faqs:
  - q: "What is precision in machine learning?"
    a: "Precision is the proportion of positive predictions that are actually correct. It is calculated as true positives divided by true positives plus false positives. High precision means the model rarely flags something as positive when it is not."
  - q: "What is recall in machine learning?"
    a: "Recall is the proportion of actual positives that the model correctly identifies. It is calculated as true positives divided by true positives plus false negatives. High recall means the model misses very few real positives."
  - q: "What is F1 score?"
    a: "F1 score is the harmonic mean of precision and recall. It provides a single metric that balances both, and is particularly useful when the dataset is imbalanced. A perfect F1 score is 1.0."
  - q: "When should I use precision vs recall?"
    a: "Optimise for precision when the cost of a false positive is high — for example, spam detection or an irrelevant recommendation. Optimise for recall when the cost of a false negative is high — for example, cancer screening or fraud detection where missing a real case is dangerous."
  - q: "What is the precision-recall tradeoff?"
    a: "Precision and recall move in opposite directions as you adjust the classification threshold. Lowering the threshold catches more positives (higher recall) but also includes more false positives (lower precision). Raising the threshold does the reverse."
  - q: "How does AWS SageMaker evaluate precision, recall, and F1?"
    a: "SageMaker's built-in binary classification algorithms report precision, recall, and F1 as standard evaluation metrics. SageMaker Clarify also uses these metrics when evaluating model fairness. You can access all three via the SageMaker console, CloudWatch, or the Experiments API."
---

**Precision**, **recall**, and **F1 score** are three metrics that measure classification model performance from different angles — and choosing the wrong one for your use case can lead to a model that looks good on paper but fails in production.

{% capture def %}
**Precision** answers: of everything the model predicted as positive, how many were actually positive? **Recall** answers: of all the real positives in the data, how many did the model find? **F1 score** is the harmonic mean of both, giving a single balanced metric. All three are derived from the confusion matrix.
{% endcapture %}
{% include callout.html type="definition" label="Definition" content=def %}

## The Confusion Matrix: Where It All Starts

All three metrics are calculated from four values:

| | Predicted Positive | Predicted Negative |
|---|---|---|
| **Actually Positive** | True Positive (TP) | False Negative (FN) |
| **Actually Negative** | False Positive (FP) | True Negative (TN) |

- **True Positive (TP)** — model predicted positive, and it was correct
- **False Positive (FP)** — model predicted positive, but it was wrong (a false alarm)
- **False Negative (FN)** — model predicted negative, but the true label was positive (a miss)
- **True Negative (TN)** — model predicted negative, and it was correct

## What is Precision?

Precision measures how trustworthy the model's positive predictions are.

> **Precision = TP ÷ (TP + FP)**

A model with high precision rarely raises a false alarm. When it says "positive", it is almost always right.

**Example:** A spam filter with 95% precision means 95% of emails it marks as spam are actually spam. Only 5% are legitimate emails incorrectly flagged.

## What is Recall?

Recall measures how well the model catches all the real positives.

> **Recall = TP ÷ (TP + FN)**

A model with high recall misses very few actual positives. It casts a wide net.

**Example:** A cancer screening model with 95% recall correctly identifies 95% of patients who have cancer. Only 5% of actual cases are missed.

## What is F1 Score?

F1 score is the harmonic mean of precision and recall.

> **F1 = 2 × (Precision × Recall) ÷ (Precision + Recall)**

The harmonic mean penalises extreme imbalance between the two. A model with 100% precision and 0% recall gets an F1 of 0 — not 50% — which is the correct reflection of its uselessness.

F1 is most useful when:
- The dataset is **imbalanced** (far more negatives than positives)
- You need a **single number** to compare models
- Both precision and recall matter, but you cannot sacrifice either

{% capture exam_tip %}
The AWS ML exam commonly presents a business scenario and asks which metric to optimise for. The key question to ask is: **which error is more costly — a false positive or a false negative?** False positive is more costly → precision. False negative is more costly → recall. Neither clearly worse → F1.
{% endcapture %}
{% include callout.html type="exam" label="Exam Tip" content=exam_tip %}

## The Precision-Recall Tradeoff

Precision and recall move in opposite directions as you adjust the **classification threshold** — the probability cutoff above which the model predicts "positive".

- **Lower the threshold** → more predictions flagged as positive → recall goes up, precision goes down
- **Raise the threshold** → fewer predictions flagged as positive → precision goes up, recall goes down

You cannot maximise both simultaneously. The right balance depends entirely on the cost of each type of error in your specific context.

## When to Optimise for Precision

Favour precision when **false positives are costly**:

- **Spam detection** — incorrectly blocking a legitimate email is worse than letting one spam through
- **Content moderation** — wrongly removing a legitimate post has reputational and legal consequences
- **Medical treatment recommendations** — prescribing unnecessary treatment carries real risk and cost
- **Ad targeting** — showing an irrelevant ad wastes money and degrades user experience

## When to Optimise for Recall

Favour recall when **false negatives are costly**:

- **Cancer screening** — missing a real case has life-or-death consequences
- **Fraud detection** — failing to catch a fraudulent transaction causes direct financial loss
- **Security threat detection** — a missed intrusion is far worse than a false alarm
- **Quality control** — letting a defective product through to customers is worse than over-inspecting

{% capture warning %}
**Accuracy is often a misleading metric** for classification problems, particularly with imbalanced datasets. A model that predicts "not fraud" for every transaction can achieve 99.9% accuracy if only 0.1% of transactions are fraudulent — while being completely useless. Always check precision and recall alongside accuracy.
{% endcapture %}
{% include callout.html type="warning" label="Common Mistake" content=warning %}

## Precision, Recall, and AWS

AWS provides direct support for these metrics across the ML stack:

- **SageMaker built-in algorithms** — binary classification algorithms such as Linear Learner and XGBoost report precision, recall, and F1 as standard evaluation outputs
- **SageMaker Clarify** — uses these metrics to evaluate model fairness across demographic groups, checking whether precision or recall differs significantly between subgroups
- **SageMaker Experiments** — lets you track and compare precision, recall, and F1 across training runs to find the best model configuration
- **Amazon Fraud Detector** — a managed service that is recall-optimised by design, since missing fraud is more costly than a false alert

When configuring Linear Learner in SageMaker, you can directly set a **target recall** or **target precision**, and the algorithm will tune the classification threshold automatically to meet it.

{% capture tip %}
**Metric selection summary:**

| Use case | Primary metric |
|---|---|
| Imbalanced dataset, both errors matter | F1 |
| False alarm is the bigger problem | Precision |
| Missing a real case is the bigger problem | Recall |
| Balanced dataset, errors cost the same | Accuracy or F1 |
{% endcapture %}
{% include callout.html type="tip" label="Quick Reference" content=tip %}

{% include key-takeaways.html items="Precision measures how often a positive prediction is correct: TP ÷ (TP + FP).|Recall measures how many real positives the model catches: TP ÷ (TP + FN).|F1 score is the harmonic mean of precision and recall — it penalises extreme imbalance between the two.|Lowering the classification threshold increases recall but reduces precision. Raising it does the reverse.|Optimise for precision when false positives are costly. Optimise for recall when false negatives are costly.|Accuracy is misleading on imbalanced datasets — always inspect precision and recall.|SageMaker Linear Learner lets you set a target precision or recall directly as a training objective." %}

{% include related-posts.html %}
{% include faq.html %}
{% include article-schema.html %}
