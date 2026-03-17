---
title: "What is Overfitting in Machine Learning? Causes, Detection, and Fixes"
date: 2026-01-30
categories: [machine-learning]
tags: [overfitting, regularisation, model-evaluation, fundamentals]
excerpt: "Overfitting is when a model learns training data too well — including its noise — and fails to generalise to new data. Here is how to detect it and fix it."
layout: single
author_profile: true
read_time: true
toc: true
toc_label: "In this article"
faqs:
  - q: "What is overfitting in machine learning?"
    a: "Overfitting is when a model learns the training data too well — including its noise and random variation — and loses the ability to generalise to new, unseen data. An overfit model has low training error but high validation and test error."
  - q: "What causes overfitting?"
    a: "Overfitting is caused by a model that is too complex relative to the amount of training data available. Common causes include too many parameters, too many features, training for too many epochs, and having too little training data to constrain the model."
  - q: "How do you detect overfitting?"
    a: "The clearest sign of overfitting is a large gap between training error and validation error — training error is low while validation error is significantly higher. Learning curves that show this divergence confirm overfitting."
  - q: "What is regularisation and how does it prevent overfitting?"
    a: "Regularisation adds a penalty term to the loss function that discourages the model from learning overly complex patterns. L1 regularisation (Lasso) can reduce some weights to zero, effectively selecting features. L2 regularisation (Ridge) shrinks all weights toward zero without eliminating them. Both reduce the model's tendency to memorise noise."
  - q: "What is the difference between overfitting and underfitting?"
    a: "Overfitting occurs when a model is too complex and memorises training data instead of learning general patterns — high training accuracy, low test accuracy. Underfitting occurs when a model is too simple to capture the real patterns — low accuracy on both training and test data."
  - q: "How does AWS SageMaker help prevent overfitting?"
    a: "SageMaker Debugger can monitor training and validation loss in real time and trigger early stopping when overfitting is detected. SageMaker Automatic Model Tuning optimises regularisation hyperparameters. Built-in algorithms like XGBoost and Linear Learner expose L1 and L2 regularisation directly as tunable parameters."
---

**Overfitting** is when a machine learning model learns the training data too well — including its noise and random variation — and loses the ability to generalise to new, unseen data.

{% capture def %}
An **overfit model** has memorised the training set rather than learned the underlying patterns. It performs well on data it has already seen and poorly on data it has not. The signature is low training error paired with significantly higher validation or test error.
{% endcapture %}
{% include callout.html type="definition" label="Definition" content=def %}

## What Causes Overfitting?

Overfitting happens when a model has too much capacity relative to the amount of training data available.

**Model complexity:** A model with many parameters — a deep neural network, a large decision tree, a high-degree polynomial — can memorise individual training examples rather than abstract the patterns behind them.

**Too little data:** Even a moderately complex model can overfit if there is not enough training data to constrain it. More examples force the model to find patterns that generalise.

**Too many features:** Features that are irrelevant or noisy give the model additional dimensions to overfit against.

**Training too long:** Gradient-based models can overfit if trained for too many iterations. Early in training, the model learns general patterns. Later, it begins fitting noise.

## How to Detect Overfitting

The clearest signal is a large gap between training error and validation error:

| Training Error | Validation Error | Diagnosis |
|---|---|---|
| Low | Low | Well-fitted model |
| Low | High | Overfitting |
| High | High | Underfitting |

**Learning curves** are the most reliable diagnostic tool. Plot training loss and validation loss against the number of training epochs or data size. Overfitting appears as the two curves diverging — training loss continues to fall while validation loss rises or plateaus.

{% capture exam_tip %}
On the AWS ML exam, overfitting scenarios are often described in terms of symptoms rather than named directly. If a question describes a model with excellent training accuracy but poor test accuracy, the answer involves reducing model complexity, adding regularisation, increasing training data, or applying early stopping.
{% endcapture %}
{% include callout.html type="exam" label="Exam Tip" content=exam_tip %}

## How to Fix Overfitting

### 1. Regularisation

Regularisation adds a penalty to the loss function that discourages the model from learning overly large weights.

**L2 regularisation (Ridge)** adds the sum of squared weights to the loss. All weights shrink toward zero, but none are eliminated. Good for situations where all features may have some relevance.

**L1 regularisation (Lasso)** adds the sum of absolute weights to the loss. Some weights are pushed to exactly zero, performing implicit feature selection. Good when you suspect many features are irrelevant.

> Increasing the regularisation strength (lambda) reduces variance at the cost of slightly higher bias.

### 2. Early Stopping

Train the model while monitoring validation loss. Stop training when validation loss stops improving — before the model begins memorising noise.

Early stopping is particularly effective for neural networks and gradient boosting models, where each additional training step increases the risk of overfitting.

### 3. Dropout (Neural Networks)

During training, randomly deactivate a proportion of neurons on each forward pass. This prevents individual neurons from becoming overly specialised and forces the network to learn redundant representations that generalise better.

A dropout rate of 0.2–0.5 is typical. Dropout is only applied during training, not inference.

### 4. Cross-Validation

Instead of using a single train/validation split, use k-fold cross-validation. The dataset is split into k subsets, and the model is trained and evaluated k times, each time using a different subset as validation.

Cross-validation gives a more reliable estimate of true generalisation performance and is less susceptible to variance in a single split.

### 5. More Training Data

More data forces the model to find patterns that hold across a wider range of examples, rather than patterns that only apply to a small set. When collecting more data is impossible, **data augmentation** — creating modified versions of existing examples — can have a similar effect.

### 6. Reduce Model Complexity

Use a simpler model: fewer layers, fewer neurons, a shallower tree, fewer polynomial degrees. The right level of complexity is the minimum needed to capture the real patterns in the data.

### 7. Feature Selection

Remove irrelevant or redundant features. Fewer input dimensions means fewer directions the model can overfit along. Techniques include correlation analysis, recursive feature elimination, and L1 regularisation.

{% capture tip %}
**Quick fix selector:**

- Neural network overfitting → dropout + early stopping
- Tree model overfitting → reduce max depth, increase min samples per leaf
- Linear model overfitting → L1 or L2 regularisation
- All models → more training data, cross-validation, feature selection
{% endcapture %}
{% include callout.html type="tip" label="Quick Fix Reference" content=tip %}

## Overfitting and AWS

AWS provides concrete tooling to address overfitting at each stage of the ML pipeline:

- **SageMaker Debugger** — monitors training and validation loss in real time during a training job. You can configure built-in rules to automatically detect overfitting and trigger a stop condition when the gap between training and validation loss exceeds a threshold.

- **SageMaker Automatic Model Tuning** — optimises hyperparameters including regularisation strength (lambda for L1/L2), dropout rate, tree depth, and number of epochs, finding the configuration that best balances bias and variance on validation data.

- **XGBoost on SageMaker** — exposes `alpha` (L1) and `lambda` (L2) regularisation, `max_depth`, `subsample`, and `colsample_bytree` — all directly relevant to controlling overfitting in gradient boosted trees.

- **Linear Learner on SageMaker** — supports L1 and L2 regularisation and can be configured to optimise directly for validation metrics.

- **Amazon SageMaker Data Wrangler** — helps with feature selection and data quality improvements that reduce the noise the model is exposed to in the first place.

{% capture warning %}
Increasing model complexity is not always the right response to poor performance. Before adding layers, features, or parameters, always confirm whether the problem is underfitting (high bias) or overfitting (high variance). The fixes are in opposite directions — applying the wrong one makes the problem worse.
{% endcapture %}
{% include callout.html type="warning" label="Common Mistake" content=warning %}

{% include key-takeaways.html items="Overfitting is when a model memorises training data including its noise, and fails to generalise — low training error, high validation error.|It is caused by excessive model complexity, too little data, too many features, or training for too long.|Detect it by comparing training and validation error — a large gap points to overfitting.|Core fixes: regularisation (L1/L2), early stopping, dropout, cross-validation, more data, simpler model.|SageMaker Debugger detects overfitting in real time during training and can trigger automatic early stopping.|Regularisation hyperparameters are exposed directly in SageMaker's XGBoost and Linear Learner algorithms." %}

{% include related-posts.html %}
{% include faq.html %}
{% include article-schema.html %}
