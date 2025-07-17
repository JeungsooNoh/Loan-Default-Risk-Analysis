
# Loan Default Risk Analysis

**Author**: Jeungsoo Noh  
**Date**: July 2025

---

## 1. Project Overview

This project develops a binary classification model to predict the risk of loan default, using historical LendingClub loan data. It simulates a real-world risk assessment task where financial institutions aim to identify high-risk borrowers prior to default, a key function in risk management and financial planning roles such as Risk Analyst or FP&A Analyst.

---

## 2. Data Summary

- **Source**: LendingClub accepted loan dataset (2007–2018) https://www.kaggle.com/datasets/wordsforthewise/lending-club
- **Sample Size**: 5,000 loans
- **Target Variable**: `loan_status`
  - Fully Paid → 0 (non-defaulter)
  - Charged Off → 1 (defaulter)
- **Removed**: Other statuses (e.g., Current, Late) excluded

---

## 3. Selected Features

A mix of financial, credit, and employment-related variables were selected:

- **Loan Terms**: `loan_amnt`, `term`, `installment`, `int_rate`
- **Credit Grades**: `grade`, `sub_grade`
- **Employment**: `emp_length`
- **Home Ownership**: `home_ownership`
- **Financial Ratios**: `annual_inc`, `dti`, `loan_amnt / annual_inc`
- **Credit History**: `fico_range_low`, `revol_util`, `inq_last_6mths`, `open_acc`, `total_acc`
- **Purpose of Loan**: `purpose`

All categorical variables were one-hot encoded and missing numeric values were imputed using the median.

---

## 4. Modeling Approach

- **Model Used**: Logistic Regression (`class_weight='balanced'`)
- **Train-Test Split**: 80:20 with stratified sampling
- **Evaluation Metrics**: Confusion matrix, classification report, ROC-AUC

---

## 5. Model Performance

| Metric           | Value  |
|------------------|--------|
| Accuracy         | 68%    |
| Precision (Class 1) | 32% |
| Recall (Class 1)    | 66% |
| F1-Score (Class 1)  | 43% |
| **AUC Score**        | **0.75** |

The model is particularly effective at capturing defaulters (66% recall), which is critical in financial risk modeling. Though precision is modest, the trade-off supports early risk flagging.

---

## 6. Top Predictive Features

### Positive Impact (Higher Default Risk):
- `int_rate`: Higher interest rate
- `inq_last_6mths`: More credit inquiries
- `open_acc`: Higher open accounts
- `home_ownership_RENT`: Renting vs owning
- `dti`: Debt-to-income ratio

### Negative Impact (Lower Default Risk):
- `fico_range_low`: Higher credit scores
- `sub_grade_A2/A3`: Strong credit
- `purpose_credit_card/home_improvement`: Responsible loan purposes
- `total_acc`: Richer credit history
- `emp_length_10+ years`: Stable employment

---

## 7. Business Relevance

This project demonstrates skills in:
- Developing interpretable risk models
- Handling class imbalance
- Translating financial variables into risk flags
- Communicating model logic to stakeholders

It simulates real work done by analysts in credit risk, financial planning, or operational finance roles.

---

## 8. Tools Used

- Python (pandas, scikit-learn, matplotlib, seaborn)
- Jupyter Notebook

---



---

## 9. Conclusion

With an AUC of 0.75 and strong recall on defaulters, this model provides meaningful predictive value while maintaining interpretability. It is suitable for showcasing applied risk modeling in a financial analyst context. 
