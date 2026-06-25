---
noteId: "29b33a1070b111f19ec49d9bd6d884a1"
tags: []

---

# Bank Marketing Response Modeling

## Project Overview

This project analyzes customer response to a bank marketing campaign and builds a predictive workflow for campaign prioritization. The dataset comes from a direct marketing campaign where the target variable `y` indicates whether the customer subscribed to the offer.

The notebook is framed as a business analytics project. It studies customer segments, campaign timing, prior outcomes, loan status, and contact behavior to understand who is more likely to respond. It also separates a with-duration model from a pre-call targeting model because `duration` is only known after the call happens.

## Problem Definition

Marketing campaigns waste resources when customers are contacted without a clear likelihood of response. A bank needs to prioritize customers who are more likely to accept an offer while managing contact cost, customer fatigue, and campaign efficiency.

The key questions are:

- Which customer groups have higher acceptance rates?
- How imbalanced is the campaign response?
- Which variables are available before the call and useful for targeting?
- How much predictive power comes from `duration`, and why should it be treated carefully?
- What threshold should be used when campaign budget or contact capacity changes?

## Dataset

The notebook uses the local CSV:

```text
data/raw/bank-full.csv
```

The dataset includes customer information, banking attributes, campaign contact details, previous campaign outcomes, and the target variable:

- `y = yes`: customer accepted/subscribed
- `y = no`: customer did not accept/subscribe

## What Is Covered

- Dataset loading from a local CSV
- Data quality audit with missing and `unknown` value review
- Target encoding for campaign acceptance
- Feature engineering for previous contact, prior campaign success, loan indicators, and age bands
- Descriptive statistics by campaign response
- Segment analysis by job, marital status, education, loan status, contact type, month, prior outcome, and age band
- Exploratory visual analytics for response balance, seasonality, job groups, age, duration, and housing-loan segments
- Statistical tests for numeric and categorical response differences
- Correlation and VIF review for multicollinearity
- VADER sentiment applicability audit
- With-duration versus pre-call model comparison
- Tuned regularized logistic regression for realistic pre-call targeting
- Confusion matrix, ROC curve, precision-recall curve, cross-validation, and threshold tradeoff analysis
- Logistic coefficient review and practical segment insight

## Key Findings

- Campaign response is highly imbalanced; most customers do not accept the offer.
- `duration` is one of the strongest predictors, but it is only known after the customer is contacted.
- A realistic pre-call targeting model should focus on variables available before outreach.
- Prior campaign outcome, contact channel, month, age, balance, and loan indicators are more useful for pre-call prioritization.
- Job groups differ in both customer volume and acceptance rate, so campaign strategy should consider both.
- Not all variables explain response equally; some are useful for segmentation but weak as direct predictive signals.
- VADER sentiment analysis is not applicable because the dataset has no call transcripts, comments, or free-text customer feedback.

## Solution Approach

The solution uses a campaign-response analytics pipeline:

1. Audit data quality and review `unknown` values.
2. Encode the campaign response target.
3. Build engineered features that support business interpretation.
4. Explore customer and campaign segments with acceptance rates.
5. Use statistical tests to identify meaningful differences between accepted and non-accepted groups.
6. Check correlation and VIF to understand overlapping numeric predictors.
7. Compare models with and without `duration`.
8. Tune a regularized logistic regression model using only realistic pre-call features.
9. Evaluate the model with classification metrics and threshold tradeoff analysis.

## Results Summary

The notebook shows that campaign modeling should be handled as a ranking and prioritization problem. A model that includes `duration` performs strongly but is not realistic for deciding whom to call. The pre-call model is more useful for real campaign planning because it uses information available before outreach.

## Business Solution

The final model can support a campaign workflow such as:

- Rank customers by predicted acceptance probability.
- Select a contact threshold based on available call capacity.
- Prioritize high-probability segments for direct outreach.
- Use lower-cost channels for medium-probability customers.
- Avoid over-contacting low-probability customers to reduce fatigue.

A stronger production version would combine acceptance probability with expected revenue, contact cost, customer lifetime value, and fatigue risk.

## Repository Structure

```text
data/raw/
  bank-full.csv
notebooks/
  05_personal_loan_acceptance_prediction.ipynb
outputs/figures/
  Exported charts from the notebook
requirements.txt
README.md
```

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook notebooks/05_personal_loan_acceptance_prediction.ipynb
```

## Conclusion

Bank marketing response modeling is most useful when it supports campaign prioritization. The final workflow identifies meaningful response signals, avoids overusing post-call `duration` for pre-call targeting, and connects model thresholds to practical campaign decisions.
