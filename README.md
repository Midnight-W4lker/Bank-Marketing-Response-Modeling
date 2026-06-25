---
noteId: "5b154d7070aa11f19ec49d9bd6d884a1"
tags: []

---

# Personal Loan / Term Deposit Acceptance Prediction

This repository contains a completed analytics notebook for predicting customer response to a bank marketing campaign. The work is framed as campaign prioritization rather than a generic classification exercise.

## What This Notebook Covers

- Dataset loading from a local CSV
- Data quality audit with missing and `unknown` value review
- Descriptive statistics by campaign response
- Segment analysis by job, marital status, education, prior outcome, loan status, contact channel, month, and age band
- Exploratory visual analytics with response balance, seasonal response, job-rate comparison, box plots, and heatmaps
- Statistical tests for numeric and categorical response differences
- Correlation and VIF review for multicollinearity
- VADER sentiment applicability audit
- With-duration versus pre-call model comparison
- Tuned regularized logistic regression for pre-call targeting
- Confusion matrix, ROC curve, precision-recall curve, cross-validation, and threshold tradeoff analysis
- Coefficient review and practical segment insight

## Main Result

The response class is imbalanced, so accuracy alone is not enough. `duration` is highly predictive but is only known after contact, so the final campaign-targeting model focuses on pre-call features such as prior outcome, contact channel, month, age, balance, and loan indicators.

## Important Note

This dataset predicts subscription response, not guaranteed long-term profitability. A mature campaign system should combine probability of acceptance with expected value, contact cost, and customer fatigue risk.

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook notebooks/05_personal_loan_acceptance_prediction.ipynb
```

The notebook expects this file:

```text
data/raw/bank-full.csv
```

Exported charts are saved in `outputs/figures/`.
