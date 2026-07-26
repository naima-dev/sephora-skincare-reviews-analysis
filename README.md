# What Actually Drives Customer Ratings in Skincare? A 1M-Review Analysis

Analysis of **1,094,411 customer reviews** and **9,168 products** from Sephora, testing which factors  brand, price, product category, or customer skin profile  actually explain customer satisfaction and recommendation behaviour.

Capstone project (INF4173), Université du Québec en Outaouais April 2026.

---

## Business question

Skincare brands invest heavily in premium positioning and in tailoring products to specific skin types. Both strategies assume those levers move customer satisfaction. This project tests that assumption against a million real reviews:

> Which factors  brand, price, category, or customer skin type — actually explain how customers rate skincare products and whether they recommend them?

## Data

| Dataset | Rows | Level | Source |
|---|---|---|---|
| Reviews | 1,094,411 | Individual review | [Sephora Products and Skincare Reviews](https://www.kaggle.com/datasets/nadyinky/sephora-products-and-skincare-reviews) (Kaggle) |
| Products | 9,168 | Product | [All Products Available on Sephora Website](https://www.kaggle.com/datasets/raghadalharbi/all-products-available-on-sephora-website) (Kaggle) |

**The raw data is not redistributed in this repository.** Download it from the Kaggle links above and place the CSV files in a `data/` folder before running the notebook. Both datasets are public and anonymised; user identifiers are opaque codes with no traceable link to real individuals.

The two sources use incompatible product identifiers and cannot be joined directly. They are analysed separately and reconciled at brand and category level  a documented constraint, not an oversight.

## Repository contents

```
├── README.md
├── requirements.txt
├── analysis.ipynb      # full pipeline: cleaning, EDA, advanced analysis, model
└── report.pdf          # full written report (French, 66 pages, all figures)
```

## Method

- **Cleaning & feature engineering** — date parsing, price bands (entry / mid / premium), sentiment labels derived from ratings
- **Exploratory analysis** — rating distributions, review volume over time, brand profiles, price–rating relationship
- **Cross-sectional analysis** — brand × skin type, satisfaction vs. recommendation mismatches, polarising products
- **NLP** — VADER sentiment scoring on a 10,000-review sample
- **Modelling** — decision tree to rank predictors of recommendation behaviour

Tools: Python (pandas, matplotlib, seaborn, scikit-learn, vaderSentiment), Power BI.

## Findings

**1. Price does not predict satisfaction.** Pearson correlation between price and rating: **0.019**. Average ratings across price bands: entry 3.90, mid 4.05, premium 4.07  a 0.17-point spread. Customers appear to scale their expectations to what they paid, cancelling out any premium advantage.

**2. Popularity does not equal perceived quality.** CLINIQUE leads on review volume (49,029 reviews) but averages 4.25/5. DAMDAM, with 1,128 reviews, averages 4.74/5. Dermalogica  a professional, therapist-recommended brand averages 4.61/5 across 24,415 reviews. Specialist brands serving a self-selected, informed audience consistently outperform mass-market brands.

**3. Skin type is not a differentiator.** Average ratings by skin type: combination 4.31, dry 4.29, normal 4.28, oily 4.27  a spread under 0.04 points, stable across every brand tested. This **contradicts** the project's initial hypothesis that sensitive-skin users would rate more harshly.

**4. Satisfaction and recommendation are distinct behaviours.** Some customers rate 4–5 stars without recommending (concentrated in premium brands Tatcha, Drunk Elephant, Estée Lauder), while others rate 1–2 stars but still recommend (concentrated in technical, active-ingredient brands like The Ordinary). Two products appear in *both* groups — Drunk Elephant Protini and LANEIGE Lip Sleeping Mask  making them the genuinely polarising items in the catalogue.

**5. What the model taught me.** A decision tree predicting recommendation reached 96% accuracy, with the rating variable accounting for 99.97% of feature importance. This is not a finding — it is **target leakage**: rating and recommendation measure the same underlying satisfaction, so the model only restates a tautology. Diagnosing this is the honest outcome. A meaningful version of this model would need to predict recommendation from product and customer attributes *only*, excluding the rating.

## What this means for the business

For **brands**: the alignment between what a product promises and what it delivers matters more than price positioning or catalogue size. A niche brand that speaks to an informed, well-matched audience earns better reviews than a mass-market brand with ten times the volume. Serving fewer, better-matched customers is a defensible strategy, not a limitation.

For **retailers**: price is not a satisfaction argument. A well-formulated $15 product earns the same rating as a $200 product that over-promises. Curating on formulation quality beats curating on price tier.

For **product and marketing teams**: dissatisfaction in skincare is rarely universal — it is a mismatch between a formulation and an individual skin profile. Technical products with concentrated actives (serums, acids, retinol) concentrate complaints not because they underperform, but because they require guidance to use correctly. Better pre-purchase guidance — a diagnostic quiz, clearer usage protocols, realistic timelines — would convert a meaningful share of one-star reviews into satisfied customers.

## Author's note

I worked as a cosmetician before moving into data. That background shaped the interpretation throughout: understanding why a polypeptide formulation triggers intolerance in some skin profiles, or why the word "dry" appears in both positive and negative reviews depending on whether it describes a skin type or a product texture, is not something the data reveals on its own.

## Author

**Naima Ait Belkacem** — Computer Science, Université du Québec en Outaouais
