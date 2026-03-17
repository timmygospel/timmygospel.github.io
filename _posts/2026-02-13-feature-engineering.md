---
title: "Feature Engineering Explained: Turning Raw Data Into Model-Ready Features"
date: 2026-02-13
categories: [machine-learning]
tags: [feature-engineering, data-preprocessing, fundamentals]
excerpt: "Feature engineering is the process of transforming raw data into input features that help machine learning models learn effectively. Better features consistently outperform more complex algorithms on the same raw data."
layout: single
author_profile: true
read_time: true
toc: true
toc_label: "In this article"
faqs:
  - q: "What is feature engineering in machine learning?"
    a: "Feature engineering is the process of transforming raw data into input features that help machine learning models learn more effectively. It includes encoding categorical variables, scaling numerical features, creating new features from existing ones, and removing irrelevant or redundant features."
  - q: "Why is feature engineering important?"
    a: "Machine learning models learn from the features they are given. Poor or uninformative features produce poor models regardless of algorithm complexity. Feature engineering directly improves the quality of information the model can use, often producing larger performance gains than switching to a more sophisticated algorithm."
  - q: "What is the difference between normalisation and standardisation?"
    a: "Normalisation (min-max scaling) rescales features to a fixed range, typically 0 to 1. Standardisation (z-score scaling) rescales features to have zero mean and unit variance. Standardisation is generally preferred for algorithms that assume normally distributed features or use distance metrics, such as linear models, SVMs, and neural networks."
  - q: "What is one-hot encoding?"
    a: "One-hot encoding converts a categorical variable into a set of binary columns — one per category. For a variable with k categories, it creates k binary features where exactly one is 1 for each example. It is used when the categories have no natural ordering."
  - q: "What is data leakage in feature engineering?"
    a: "Data leakage occurs when information from outside the training set is used to create features — for example, computing a scaling factor from the full dataset including the test set. This produces artificially inflated performance estimates that do not hold on truly unseen data."
  - q: "How does AWS support feature engineering?"
    a: "AWS offers SageMaker Data Wrangler for visual, code-free feature engineering, SageMaker Processing Jobs for running custom transformation scripts at scale, and SageMaker Feature Store for storing, versioning, and sharing features across teams and models."
---

**Feature engineering** is the process of transforming raw data into input features that help machine learning models learn effectively — and it is often where the largest real-world performance gains come from.

{% capture def %}
**Feature engineering** covers every transformation applied to raw data before it reaches a model: encoding categorical variables, scaling numerical values, creating new features from existing ones, and removing irrelevant or redundant information. The goal is to give the model the cleanest, most informative representation of the data possible.
{% endcapture %}
{% include callout.html type="definition" label="Definition" content=def %}

## Why Feature Engineering Matters

Machine learning models do not see data — they see numbers. The quality of those numbers determines the quality of what the model can learn.

A well-engineered feature set can make a simple linear model outperform a complex deep network on the same raw data. Conversely, no amount of algorithmic sophistication compensates for features that are noisy, irrelevant, or badly encoded.

The practitioner maxim holds: **garbage in, garbage out**.

## Encoding Categorical Variables

Most ML algorithms require numerical inputs. Categorical variables — colours, countries, product types — need to be converted.

### One-Hot Encoding

Creates one binary column per category. Exactly one column is 1 for each example.

> Country: [UK, US, DE] → `is_UK`, `is_US`, `is_DE`

**When to use:** Unordered categories with a manageable number of unique values (low cardinality). Suitable for linear models, SVMs, and neural networks.

**Watch out for:** High-cardinality variables (e.g. postcode, user ID) create thousands of sparse columns and can hurt performance.

### Label Encoding

Assigns an integer to each category: UK=0, US=1, DE=2.

**When to use:** Only for tree-based models (decision trees, random forests, XGBoost) which can handle arbitrary integer codes without implying order. Do not use for linear models — the integer implies a false ordering.

### Target Encoding

Replaces each category with the mean target value for that category across the training set.

**When to use:** High-cardinality categorical variables where one-hot encoding would create too many columns. Requires careful cross-validation to avoid leakage.

{% capture exam_tip %}
The AWS ML exam tests knowledge of when to use different encoding strategies. The key distinctions: one-hot for low-cardinality unordered categories, label encoding for tree models, target encoding for high-cardinality variables. SageMaker's built-in algorithms handle some encoding automatically, but custom preprocessing is common in SageMaker Processing Jobs.
{% endcapture %}
{% include callout.html type="exam" label="Exam Tip" content=exam_tip %}

## Scaling Numerical Features

Many algorithms — linear models, SVMs, k-nearest neighbours, neural networks — are sensitive to the scale of input features. A feature measured in thousands will dominate one measured in fractions unless both are rescaled.

### Min-Max Normalisation

Rescales each feature to the range [0, 1].

> x_scaled = (x − min) / (max − min)

**When to use:** When you need a bounded output range. Commonly used in neural networks.

**Watch out for:** Sensitive to outliers — a single extreme value compresses all other values into a narrow band.

### Standardisation (Z-Score Scaling)

Rescales each feature to have zero mean and unit variance.

> x_scaled = (x − mean) / standard deviation

**When to use:** Most linear models, SVMs, neural networks, and any algorithm that uses distance or gradient descent. The default choice when in doubt.

**Note:** Tree-based models (decision trees, random forests, XGBoost) do not require scaling — they split on thresholds, not magnitudes.

### Log Transformation

Applies a logarithm to compress right-skewed distributions.

**When to use:** Features with a long right tail — income, population, web traffic counts. Brings the distribution closer to normal and reduces the influence of extreme values.

## Feature Creation

New features can encode relationships that raw columns do not express directly.

**Interaction terms** — multiply two features together to capture their combined effect. A model may not detect that the combination of `age × income` predicts behaviour if it can only see each variable separately.

**Polynomial features** — add squared or cubed versions of numerical features to let linear models fit non-linear relationships.

**Date decomposition** — extract year, month, day of week, hour, or season from datetime columns. A model cannot compute "this sale happened on a Friday" from a raw timestamp.

**Ratio features** — divide one feature by another. Revenue per user, clicks per impression, and similar ratios often have stronger predictive power than either raw value.

## Feature Selection

Not all features help. Irrelevant or redundant features increase noise, training time, and the risk of overfitting.

**Correlation analysis** — remove features that are highly correlated with each other (multicollinearity). Two features that say the same thing add noise, not signal.

**Feature importance** — tree-based models output a feature importance score after training. Low-importance features can be dropped without significantly affecting performance.

**L1 regularisation (Lasso)** — adds a penalty that pushes some feature weights to exactly zero, performing implicit feature selection during training.

**Recursive Feature Elimination (RFE)** — iteratively removes the least important features and retrains the model until a target number of features is reached.

{% capture tip %}
**Feature engineering order of operations:**
1. Handle missing values
2. Encode categorical variables
3. Scale numerical features
4. Create new features
5. Select the best subset
{% endcapture %}
{% include callout.html type="tip" label="Order of Operations" content=tip %}

## Handling Missing Values

Real-world data is rarely complete. Missing values need to be addressed before training.

**Mean/median imputation** — replace missing numerical values with the column mean or median. Median is more robust to outliers.

**Mode imputation** — replace missing categorical values with the most frequent category.

**Indicator imputation** — add a binary `is_missing` column alongside the imputed value. This preserves the information that data was missing, which can itself be predictive.

**Drop rows or columns** — appropriate when missingness is extensive and not recoverable.

{% capture warning %}
Fit all imputers and scalers on training data only. Never compute statistics (mean, min, max, standard deviation) from the full dataset including the test or validation set. Doing so is data leakage — the model indirectly sees test data during training, producing falsely optimistic performance estimates.
{% endcapture %}
{% include callout.html type="warning" label="Data Leakage Warning" content=warning %}

## Feature Engineering on AWS

AWS provides dedicated tooling for feature engineering at every scale:

- **SageMaker Data Wrangler** — a visual, no-code interface for exploring data and building feature transformation pipelines. Supports 300+ built-in transforms and can export pipelines to SageMaker Processing Jobs or Pipelines.

- **SageMaker Processing Jobs** — run custom Python (pandas, scikit-learn, Spark) transformation scripts at scale on S3 data. The standard way to implement feature engineering in a production ML pipeline on AWS.

- **SageMaker Feature Store** — a centralised repository for storing, versioning, and sharing features across teams and models. Supports both online (low-latency) and offline (training) feature retrieval. Prevents teams from independently recomputing the same features.

- **AWS Glue** — serverless data transformation service for large-scale ETL pipelines that feed feature data into SageMaker.

{% include key-takeaways.html items="Feature engineering transforms raw data into the input features a model uses to learn — it is often the highest-leverage part of the ML workflow.|Use one-hot encoding for low-cardinality unordered categories; label encoding for tree models; target encoding for high-cardinality variables.|Standardisation (z-score scaling) is the default scaling choice for linear models, SVMs, and neural networks. Tree models do not require scaling.|Never fit preprocessing transformations on data that includes the test set — this is data leakage.|Feature selection removes irrelevant or redundant features — reducing noise, training time, and overfitting risk.|On AWS, use SageMaker Data Wrangler for visual feature engineering, Processing Jobs for custom pipelines, and Feature Store to share features across teams." %}

{% include related-posts.html %}
{% include faq.html %}
{% include article-schema.html %}
