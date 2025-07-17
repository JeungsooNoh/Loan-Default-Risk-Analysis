# Loan Default Risk Analysis

**Author**: Jeungsoo Noh\
**Date**: July 2025

---

## 1. Project Overview

This project develops a binary classification model to predict the risk of loan default, using historical LendingClub loan data. It simulates a real-world risk assessment task where financial institutions aim to identify high-risk borrowers prior to default, a key function in risk management and financial planning roles such as Risk Analyst or FP&A Analyst.

---

## 2. Data Summary

- **Source**: LendingClub accepted loan dataset (2007–2018)
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

| Metric              | Value    |
| ------------------- | -------- |
| Accuracy            | 68%      |
| Precision (Class 1) | 32%      |
| Recall (Class 1)    | 66%      |
| F1-Score (Class 1)  | 43%      |
| **AUC Score**       | **0.75** |

### Confusion Matrix:

```
              precision    recall  f1-score   support

           0       0.90      0.68      0.78       728
           1       0.32      0.66      0.43       163

    accuracy                           0.68       891
   macro avg       0.61      0.67      0.60       891
weighted avg       0.79      0.68      0.71       891

[[498 230]
 [ 56 107]]
```

### ROC Curve:

The ROC curve illustrates the model's ability to discriminate between classes. An AUC score of **0.75** reflects solid predictive performance in identifying defaulters.



---

## 6. Top Predictive Features

### Positive Impact (Higher Default Risk):

| Feature                      | Coefficient | Interpretation                                                                                                      |
| ---------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------- |
| `int_rate`                   | **0.170**   | Higher interest rates signal higher borrower risk. Often, high-risk borrowers are charged higher rates.             |
| `inq_last_6mths`             | **0.043**   | A greater number of credit inquiries in the past six months may reflect financial distress or a need for liquidity. |
| `open_acc`                   | **0.040**   | A higher number of open credit lines could indicate overextension.                                                  |
| `home_ownership_RENT`        | **0.033**   | Renters may have more unstable housing or financial situations compared to homeowners.                              |
| `dti`                        | **0.019**   | A higher debt-to-income ratio reflects lower disposable income, increasing the likelihood of default.               |
| `purpose_debt_consolidation` | **0.014**   | Borrowers seeking to consolidate debt may already be struggling with repayment, indicating elevated risk.           |
| `grade_D`                    | **0.013**   | D-grade loans are typically riskier and carry a higher probability of default.                                      |
| `grade_B`                    | **0.010**   | B-grade borrowers also pose moderate risk relative to top-tier borrowers.                                           |
| `term_ 60 months`            | **0.009**   | Longer loan terms often correlate with higher risk due to greater uncertainty over time.                            |
| `sub_grade_C4`               | **0.008**   | Lower sub-grade loans like C4 are statistically more likely to default.                                             |

### Negative Impact (Lower Default Risk):

| Feature                                | Coefficient         | Interpretation                                                                                  |
| -------------------------------------- | ------------------- | ----------------------------------------------------------------------------------------------- |
| `fico_range_low`                       | **-0.004**          | Higher credit scores correlate with lower default risk.                                         |
| `sub_grade_A2/A3`                      | **-0.006 / -0.003** | High sub-grade borrowers are historically safer.                                                |
| `purpose_credit_card/home_improvement` | **-0.006 / -0.005** | These purposes suggest structured financial planning or necessary spending, which reduces risk. |
| `total_acc`                            | **-0.012**          | A higher number of total accounts often signals long-standing and diverse credit history.       |
| `emp_length_10+ years`                 | **-0.007**          | Longer employment tenure usually implies job stability, a protective factor.                    |

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

## 9. Potential improvement

- Test alternative models (e.g., XGBoost) if needed
- Improve class precision using threshold tuning or ensemble methods


---

## 10. Conclusion

With an AUC of 0.75 and strong recall on defaulters, this model provides meaningful predictive value while maintaining interpretability. It is suitable for showcasing applied risk modeling in a financial analyst context.

---

