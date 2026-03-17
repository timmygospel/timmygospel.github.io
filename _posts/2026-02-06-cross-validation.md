---
title: "What is Cross-Validation? Getting an Honest Estimate of Model Performance"
date: 2026-02-06
categories: [machine-learning]
tags: [model-evaluation, cross-validation, fundamentals]
excerpt: "Cross-validation estimates how well a model generalises to unseen data by training and evaluating it multiple times on different data subsets. It gives a far more reliable performance estimate than a single train-test split."
layout: single
author_profile: true
read_time: true
toc: true
toc_label: "In this article"
faqs:
  - q: "What is cross-validation in machine learning?"
    a: "Cross-validation is a technique for estimating how well a model will perform on unseen data. It works by splitting the dataset into multiple subsets, training the model on some subsets and evaluating it on others, then averaging the results across all iterations to produce a reliable performance estimate."
  - q: "What is k-fold cross-validation?"
    a: "K-fold cross-validation splits the dataset into k equal subsets (folds). The model is trained k times — each time using k-1 folds for training and the remaining fold for evaluation. The final score is the average across all k evaluations. Common values for k are 5 and 10."
  - q: "What is stratified k-fold cross-validation?"
    a: "Stratified k-fold cross-validation ensures that each fold preserves the same class distribution as the full dataset. This is important for imbalanced datasets where a random split might produce folds that are unrepresentative of the overall class balance."
  - q: "Why is cross-validation better than a single train-test split?"
    a: "A single train-test split produces a performance estimate that depends heavily on which examples happen to end up in the test set. Cross-validation averages over multiple splits, producing a lower-variance estimate that is more representative of the model's true generalisation ability."
  - q: "Does AWS SageMaker support cross-validation?"
    a: "SageMaker does not perform k-fold cross-validation automatically in its built-in training jobs. You can implement it manually using SageMaker Processing Jobs to split the data and run multiple training jobs, tracking results with SageMaker Experiments. SageMaker Automatic Model Tuning uses a held-out validation set rather than k-fold CV."
---

**Cross-validation** is a technique for estimating how well a machine learning model generalises to unseen data — by training and evaluating it multiple times on different subsets of the available data.

{% capture def %}
**Cross-validation** addresses the unreliability of a single train-test split. Instead of evaluating on one fixed holdout set, it rotates which data is used for training and which is used for evaluation across multiple rounds, then averages the results. The output is a more honest estimate of real-world performance.
{% endcapture %}
{% include callout.html type="definition" label="Definition" content=def %}

## Why a Single Train-Test Split is Not Enough

The simplest evaluation strategy is to split your data into a training set and a test set, train on one and evaluate on the other.

The problem: the result depends heavily on which examples happen to land in each split.

If your test set contains easy examples, the model looks better than it is. If it contains hard examples, it looks worse. With small datasets especially, a single split gives a high-variance estimate that is difficult to trust.

Cross-validation solves this by averaging performance across multiple different splits, reducing the luck factor.

## How K-Fold Cross-Validation Works

K-fold cross-validation is the most widely used form. The process:

1. Split the dataset into **k equal subsets** (called folds)
2. Train the model **k times** — each time using k-1 folds as training data and the remaining fold as the validation set
3. Record the evaluation metric for each run
4. **Average the k scores** to produce the final performance estimate

The model is trained k times in total, each time seeing a slightly different dataset and being evaluated on a different holdout set.

**Common values of k:** 5 and 10 are standard. Higher k gives a less biased but more computationally expensive estimate.

{% capture exam_tip %}
The AWS ML exam may ask which validation strategy to use in a given scenario. For small datasets where every example matters: k-fold cross-validation. For imbalanced classification problems: stratified k-fold. For large datasets where training is expensive: a single train/validation/test split is acceptable and practical.
{% endcapture %}
{% include callout.html type="exam" label="Exam Tip" content=exam_tip %}

## Stratified K-Fold: Preserving Class Balance

Standard k-fold assigns examples to folds randomly. On an imbalanced dataset — where one class is rare — some folds may contain very few or no examples of the minority class.

**Stratified k-fold** solves this by ensuring each fold contains approximately the same proportion of each class as the full dataset.

**When to use it:** Classification problems with imbalanced classes. It is almost always preferable to standard k-fold for classification tasks.

## Leave-One-Out Cross-Validation (LOOCV)

Leave-one-out is the extreme case: k equals the number of examples in the dataset. Each iteration trains on all data except one example, then evaluates on that single example.

**Advantages:** Nearly unbiased estimate of generalisation error. Uses almost all available data for training at each step.

**Disadvantages:** Computationally very expensive for large datasets. High variance in the estimate — individual examples have an outsized influence.

**When to use it:** Very small datasets (fewer than a few hundred examples) where every data point counts.

## Hold-Out Validation (Train / Validation / Test)

The simplest form: split data into three fixed sets — training, validation, and test.

- **Training set** — used to fit the model
- **Validation set** — used to tune hyperparameters and compare model variants
- **Test set** — used once at the very end to estimate final performance

This is the standard approach for large datasets and deep learning, where running k full training jobs is prohibitively expensive.

{% capture tip %}
**Quick guide to choosing a validation strategy:**

| Situation | Strategy |
|---|---|
| Small dataset | K-fold (k=5 or 10) |
| Imbalanced classes | Stratified k-fold |
| Very small dataset (<200 rows) | Leave-one-out |
| Large dataset / expensive training | Train / validation / test split |
{% endcapture %}
{% include callout.html type="tip" label="Quick Reference" content=tip %}

## A Common Mistake: Leaking the Test Set

Cross-validation only gives an honest estimate if the test fold is truly held out during training.

A frequent error is fitting preprocessing steps — scalers, encoders, imputers — on the **full dataset** before splitting. This leaks information from the validation fold into the training process and produces an optimistic, unreliable estimate.

The correct approach is to fit all preprocessing inside the cross-validation loop, using only the training folds.

{% capture warning %}
Never fit your scaler, encoder, or imputer on the full dataset before cross-validation. Fit them only on the training folds within each CV iteration. Preprocessing on all data before splitting is **data leakage** and will inflate your performance estimates.
{% endcapture %}
{% include callout.html type="warning" label="Data Leakage Warning" content=warning %}

## Cross-Validation on AWS

SageMaker does not perform k-fold cross-validation automatically within a single training job. The standard approach on AWS is:

- **SageMaker Processing Jobs** — use a Processing Job to split the dataset into k folds and write them to S3
- **SageMaker Training Jobs** — run k training jobs, one per fold, each pointing to the corresponding train/validation split
- **SageMaker Experiments** — track the k runs as trials within a single experiment, then compare and average results

For hyperparameter tuning, **SageMaker Automatic Model Tuning** uses a held-out validation set rather than k-fold CV. This is the practical trade-off at scale — k-fold would multiply training costs by k for every hyperparameter configuration tested.

{% include key-takeaways.html items="Cross-validation estimates generalisation performance by training and evaluating the model multiple times on different data subsets — it is more reliable than a single split.|K-fold CV splits data into k folds and rotates which fold is the validation set across k training runs. k=5 or k=10 are standard choices.|Stratified k-fold preserves class distribution in each fold — use it for classification, especially with imbalanced datasets.|LOOCV is unbiased but expensive — only use it for very small datasets.|Never fit preprocessing on the full dataset before cross-validation — this is data leakage that inflates performance estimates.|On AWS, implement k-fold CV using SageMaker Processing Jobs and Training Jobs, tracking results with SageMaker Experiments." %}

{% include related-posts.html %}
{% include faq.html %}
{% include article-schema.html %}
