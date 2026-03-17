
What you are building

A mobile-first editorial blog about machine learning and AWS exam prep that does two jobs:

proves to employers that you understand ML concepts and AWS services,

helps you remember what you learn by turning revision into published notes.

So the site should feel like a professional technical publication, not a personal diary.

The Smashing-style direction

Do not copy Smashing Magazine. Instead, borrow the qualities that make it work:

editorial homepage with featured articles and strong visual hierarchy,

excellent readability,

clear sectioning and scanning,

generous spacing,

thoughtful typography,

accessible navigation,

fast loading and stable layout,

subtle personality rather than flashy effects.

Vitaly-style guidance would be: make it useful, warm, memorable, and human. Rachel-style guidance would be: let layout do the heavy lifting with clean HTML and modern CSS, especially Grid for page structure and Flexbox for smaller UI patterns.

Recommended site structure

Use these core pages:

Home

Articles

AWS ML Exam Notes

Topics

About

Hire Me / Contact

Home page

Should include:

hero intro: who you are, what the blog covers, what exam you’re preparing for

featured post

latest posts

topic clusters such as:

Supervised Learning

Unsupervised Learning

Deep Learning

MLOps

AWS SageMaker

Exam Notes

a “Start here” block for employers/recruiters

newsletter or RSS signup if you want one later

Article pages

Every article should have:

strong title

short standfirst / deck

reading time

publish and updated date

table of contents for long posts

callout boxes for exam tips / definitions / pitfalls

author box

related posts

previous / next navigation

Best content angle for employers

Write posts in layers:

Concept — explain the idea simply.

AWS mapping — connect it to SageMaker, IAM, S3, feature engineering, pipelines, deployment, monitoring.

Exam angle — what AWS may test.

Practical angle — when you’d use it in a real project.

That makes each post useful both as revision and as a portfolio artifact.

Examples:

“Bias vs Variance Explained for the AWS ML Exam”

“When To Use SageMaker Processing vs Training Jobs”

“Precision, Recall, F1: The Practical Trade-Offs Employers Actually Care About”

“How I’d Design a Simple ML Pipeline on AWS”

“Feature Engineering Notes I Want To Remember”

UX advice for your developer
1. Mobile-first really means content-first

Start with narrow screens first. One clean column. No sidebars on mobile. Navigation, search, TOC, and related posts should collapse elegantly.

2. Make reading effortless

Use a comfortable reading width on desktop, but don’t stretch lines too far. Smashing-style sites feel editorial because text is easy to read, not because they are overly decorated.

3. Build a predictable hierarchy

Readers should instantly see:

site title / purpose,

current section,

article title,

summary,

content headings,

calls to action.

4. Design for scanning

Technical readers scan before they commit. Use:

descriptive headings,

summary boxes,

code/result/output sections,

diagrams,

“key takeaway” blocks,

short paragraphs.

5. Let layout be structural, not decorative

This is where Rachel Andrew’s influence fits perfectly: Grid for macro layout, Flexbox for local alignment, semantic HTML first, then CSS.

6. Keep interactions calm

No heavy animation. No distracting hover tricks. Use subtle transitions only where they improve comprehension.

7. Accessibility is part of polish

Use semantic headings, visible focus states, good contrast, proper landmarks, skip links, and sensible link states.

8. Performance matters

Smashing has long emphasized loading the core experience first and layering enhancements after that. On GitHub Pages, that means lean CSS, minimal JS, optimized images, and avoiding over-engineered front-end behavior.

CSS / HTML guidance for the build

Tell your developer to work like this:

HTML

Use semantic structure:

header

nav

main

article

aside only when truly secondary

footer

Inside articles:

one h1

nested h2/h3

figure/figcaption

blockquote

time

definition or note components with meaningful markup

CSS

Use:

CSS Grid for page shells, article layouts, card grids

Flexbox for nav rows, meta rows, tag lists, button groups

CSS custom properties for spacing, type scale, colors, radii

fluid typography with clamp()

container-width rules for readable measure

position: sticky for desktop TOC only if it remains unobtrusive

careful breakpoint system based on content, not device names

A solid layout pattern would be:

mobile: one column

tablet: content column + optional supporting blocks

desktop: main article + sticky TOC / sidebar

Design system suggestions

Keep the design system small and repeatable.

Core components

article card

featured article card

topic tag

author card

note / warning / exam-tip callout

code block

table of contents

pagination

newsletter/signup block

related posts module

Visual style

Smashing-inspired, but your own brand:

warm but restrained color palette

high-contrast text

large, confident headings

slightly expressive accent color

generous whitespace

editorial card layout

illustrated/diagram-led thumbnails where possible

Best Jekyll approach with Minimal Mistakes

Minimal Mistakes is intentionally minimal and meant to be customized. For GitHub Pages, using it as a remote theme is the cleanest route.

Your developer should:

keep the theme as the base,

override layouts/includes only where needed,

add custom SCSS for branding and layout,

avoid fighting the theme everywhere.

That means:

customize homepage layout first,

customize article layout second,

leave the rest of the theme mostly intact,

add a few reusable include components instead of rewriting everything.

What to avoid

trying to clone Smashing 1:1

too many homepage modules

sidebar-heavy mobile layouts

tiny text

long lines on desktop

too many tag colors

dark-pattern newsletter popups

large JS bundles

over-customizing Minimal Mistakes until upgrades become painful

A practical build plan

Phase 1:

set up Minimal Mistakes on GitHub Pages

define typography, spacing, colors

build custom homepage

build improved article template

Phase 2:

add topic pages

add TOC, related posts, callouts

improve About / Hire Me page

add structured metadata and SEO basics

Phase 3:

add search, diagrams, series pages, and polished recruiter journey

Copy-and-paste brief for your frontend developer

Build a mobile-first technical blog on GitHub Pages using Jekyll and the Minimal Mistakes theme as a base. The visual direction should be inspired by editorial tech publications like Smashing Magazine: strong typography, generous whitespace, clear hierarchy, accessible navigation, and fast performance. Use semantic HTML, CSS Grid for page-level layout, Flexbox for small UI patterns, and keep JavaScript minimal. Prioritize readability, scanning, and accessibility. The homepage should feature selected articles, topic clusters, and a clear “start here” path for recruiters. Article pages should support long-form reading with standfirst, metadata, table of contents, callout boxes, related posts, and clean code/example sections. Avoid cloning Smashing directly; aim for an original site with a similar level of editorial polish.
Got it — you want this to feel like a true machine learning publication, not an AWS-only niche site.

So we’ll reframe the entire structure to:
👉 ML-first
👉 AWS as one category within it
👉 Strong academic + practical authority (like Smashing, but for ML)

Here’s your clean Markdown structure (updated properly):

# 🧠 Machine Learning Publication (Jekyll Structure)

A scalable, editorial-style Jekyll structure focused on **machine learning concepts, intuition, and real-world applications**, with AWS as a supporting category — not the core.

---

## 📁 Root Structure


ml-blog/
├── _config.yml
├── index.html
├── about.md
├── guides.html
├── articles.html
├── topics.html
├── resources.html
├── assets/
├── _data/
├── _includes/
├── _layouts/
├── _posts/
├── _guides/
├── _topics/
├── _resources/
├── _sass/
└── .github/


---

## 📦 Content Collections

### 📝 Articles (Core Content Engine)


_posts/
├── 2026-03-17-feature-engineering-explained.md
├── 2026-03-18-bias-vs-variance.md
├── 2026-03-19-confusion-matrix.md
└── 2026-03-20-data-leakage.md


**Purpose:**
- Explain ML concepts clearly
- Rank for search + AI answers
- Build authority over time

---

### 📚 Guides (Deep Learning Paths)


_guides/
├── machine-learning-fundamentals.md
├── supervised-learning-complete-guide.md
├── model-evaluation-guide.md
├── feature-engineering-guide.md
└── deep-learning-introduction.md


**Purpose:**
- Long-form, evergreen content
- Structured learning journeys
- Your "pillar" content

---

### 🧩 Topics (Your Knowledge Graph)


_topics/
├── feature-engineering.md
├── model-evaluation.md
├── deep-learning.md
├── statistics.md
├── data-preprocessing.md
└── ml-in-aws.md


Each topic page:
- Explains the concept briefly
- Lists all related content

👉 This builds **topical authority (huge for SEO)**

---

### 📦 Resources (Practical + Tools)


_resources/
├── ml-cheat-sheet.md
├── evaluation-metrics-table.md
├── aws-ml-services-overview.md
└── ml-study-roadmap.md


**Purpose:**
- High-shareability content
- Backlink magnets
- Quick reference material

---

## 🎨 Layouts


_layouts/
├── default.html
├── home.html
├── page.html
├── post.html
├── guide.html
├── topic.html
└── archive.html


---

## 🧩 Includes (Reusable Components)


_includes/
├── head.html
├── header.html
├── footer.html
├── nav.html
├── hero.html
├── post-card.html
├── topic-pill.html
├── toc.html
├── related-posts.html
├── newsletter.html
├── faq-schema.html
└── article-schema.html


---

## ⚙️ Data Files


_data/
├── navigation.yml
├── topics.yml
└── site_settings.yml


### Navigation Example

```yaml
main:
  - title: Home
    url: /
  - title: Guides
    url: /guides/
  - title: Articles
    url: /articles/
  - title: Topics
    url: /topics/
  - title: Resources
    url: /resources/
  - title: About
    url: /about/
🎯 Assets
assets/
├── css/
│   └── main.scss
├── js/
│   └── main.js
├── images/
│   ├── site/
│   ├── diagrams/
│   └── posts/
└── fonts/
🎨 Sass Structure
_sass/
├── _variables.scss
├── _base.scss
├── _layout.scss
├── _components.scss
├── _utilities.scss
└── _syntax.scss
⚙️ Configuration (_config.yml)
title: "Machine Learning Notes"
description: "Machine learning explained clearly — from fundamentals to real-world systems."

collections:
  guides:
    output: true
    permalink: /guides/:title/
  topics:
    output: true
    permalink: /topics/:title/
  resources:
    output: true
    permalink: /resources/:title/

defaults:
  - scope:
      type: posts
    values:
      layout: post
      toc: true
  - scope:
      type: guides
    values:
      layout: guide
      toc: true
  - scope:
      type: topics
    values:
      layout: topic
  - scope:
      type: resources
    values:
      layout: page
🏠 Homepage Structure (Editorial Style)

Your homepage should feel like:

👉 A learning magazine, not a blog

Sections:

Hero (featured article)

Latest Articles (grid)

Core Guides

Topics (clickable)

Resources

Learning Paths (optional later)

🧠 Content Philosophy
1. Teach Concepts First

Not tools first

Not AWS first

2. Use AWS as Context (Not Core)

Example:

“Feature Engineering Explained”
→ includes AWS example
→ but not AWS-focused

3. Build a Knowledge Graph

Everything connects:

Articles → Guides

Guides → Topics

Topics → Articles

🔗 Internal Linking Strategy

Every article should:

Link → 1 guide

Link → 1 topic page

Link → 2–3 related articles

🚀 Outcome

This structure gives you:

Authority in machine learning (not just AWS)

Better long-term SEO potential

Strong learning experience

Smashing Magazine–style editorial system

👉 Next Steps

Create your first 3 articles

Build 1 pillar guide

Set up homepage grid layout

Start internal linking immediately


---

This version sets you up to become:

👉 **“the ML blog people trust”**  
—not just another AWS certification site.

👉 Don’t “game SEO” — build an authoritative, user-first content machine that naturally ranks.

Let’s break this into practical, modern SEO + AEO (Answer Engine Optimization) steps tailored specifically for your machine learning + AWS exam blog.

🧠 1. Start with Positioning (This is what most people skip)

Instead of:

“A blog about machine learning”

You want:

“The best resource for passing the AWS Machine Learning Specialty exam (MLS-C01/MLS-C02) with real understanding.”

That gives you:

Clear audience (aspiring ML engineers)

Clear intent (pass exam + understand ML)

Clear keyword universe

🔍 2. SEO Strategy (Dharmesh-style: inbound + compounding content)
A. Pillar + Cluster Model (CRITICAL)

Create 1 main pillar page:

👉 “AWS Machine Learning Certification — Complete Guide (2026)”

Then surround it with clusters:

Feature engineering explained (AWS exam version)

SageMaker deep dive

Bias vs variance (with AWS examples)

Data leakage explained

Model evaluation metrics cheat sheet

Real exam questions breakdown

Each post:

Links back to pillar

Links to each other

👉 This builds topical authority (Google LOVES this)

B. Keyword Strategy (Don’t overcomplicate)

Focus on:

“aws machine learning exam tips”

“sagemaker explained simply”

“feature engineering aws example”

“ml exam cheat sheet”

“ml concepts explained for beginners”

👉 Prioritize:

Low competition + high intent

Long-tail queries

🧠 3. AEO (Answer Engine Optimization — THIS is the edge now)

You’re not just ranking for Google anymore.

You’re optimizing for:

ChatGPT

Perplexity

Google SGE

Do this:
✅ Write in answer-first format

Example:

Bad:

“Feature engineering is an important concept…”

Better:

“Feature engineering is the process of transforming raw data into meaningful inputs that improve model performance.”

✅ Use structured sections

What is X?

Why it matters

Example

AWS context

Exam tip

👉 LLMs LOVE structured content

✅ Add “definition blocks”

Definition: Feature engineering is…

This gets picked up directly in AI answers.

✅ Use FAQ sections (VERY powerful)

At the bottom of each post:

What is feature engineering in AWS?

Is feature scaling required for SageMaker?

What comes up in the AWS ML exam?

👉 Helps with:

Featured snippets

AI summaries

🧱 4. Technical SEO (Perfect for your Jekyll + GitHub Pages setup)

Good news: your stack is already lightweight 👍

Must-do:
✅ Fast loading (you’re already winning here)

Minimal JS

Optimized images

Use system fonts or fast-loading web fonts

✅ Proper HTML semantics

Tell your dev:

<article> for posts

<section> for logical blocks

<h1> → single per page

<h2> → main sections

<h3> → subsections

✅ Metadata

Each post must have:

Title (keyword included)

Meta description

Open Graph tags (for sharing)

✅ Clean URLs
/aws-ml/feature-engineering/
/aws-ml/sagemaker-guide/
✅ Schema Markup (huge for AEO)

Add:

Article

FAQPage

This boosts visibility in:

Google rich results

AI extraction

✍️ 5. Content Style (This is where you win)

Think:
👉 Smashing Magazine × AWS docs × exam prep

Key traits:
✅ Teach like a human

Use analogies

Use diagrams (later)

Avoid jargon overload

✅ Show thinking, not just facts

Instead of:

“Use cross-validation”

Say:

“In the AWS exam, cross-validation is often tested when the dataset is small — it helps prevent overfitting.”

✅ Add “Exam Insight” sections

🔥 This is your differentiator

Example:

Exam Insight: AWS often tests confusion matrix interpretation rather than formula memorization.

🔗 6. Backlinks (Dharmesh-style growth)

You don’t need spammy links.

Instead:

Do this:

Post on Reddit (r/MachineLearning, r/AWSCertifications)

Share on LinkedIn (weekly insights)

Write 1–2 guest posts

Answer questions on Stack Overflow / forums

👉 Link back naturally

📈 7. Consistency Engine

Dharmesh would emphasize:

👉 Consistency > perfection

Plan:

2 posts per week

1 deep guide per month

Update old posts regularly

🧠 8. “Compounding Value” Strategy

Every post should:

Link to 3–5 related posts

Be updated over time

Improve based on feedback

👉 Over time:
You don’t just have posts — you have a learning system

⚡ Final Mindset (This is the real secret)

If Dharmesh Shah were guiding this:

He’d say:

“Don’t try to rank. Try to be the best answer on the internet for a specific problem.”