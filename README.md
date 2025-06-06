# Telco Customer Churn & Growth Analytics

This notebook presents a full analytics pipeline to explore, simulate, and model customer churn using the **Telco Customer Churn dataset**. The goal is to analyze growth and retention patterns, test strategies to reduce churn, and build a predictive model to identify at-risk customers.

---

## Contents

1. [Exploratory Data Analysis (EDA)](#-1-exploratory-data-analysis-eda)
2. [Cohort & Retention Analysis](#-2-cohort--retention-analysis)
3. [Funnel Analysis](#-3-funnel-analysis)
4. [Simulated A/B Test](#-4-simulated-ab-test)
5. [Churn Prediction Model](#-5-churn-prediction-model)

---

## Dataset

The Telco Customer Churn dataset contains 7,043 records with customer demographics, account info, service usage, and churn status.  
**Target Variable**: `Churn` (Yes/No)  
**Source**: [Kaggle Telco Dataset](https://www.kaggle.com/blastchar/telco-customer-churn)

---

## 1. Exploratory Data Analysis (EDA)

- Checked dataset shape, column types, and null values.
- Churn rate observed at ~26.5%.
- Churn varies strongly by **Contract Type** and **Tenure**.
- Created basic distribution plots for tenure and churn patterns.

---

## 2. Cohort & Retention Analysis

- Simulated `signup_date` using tenure and a reference date (`2020-02-01`).
- Grouped customers into monthly cohorts.
- Calculated monthly retention rates over 6+ years.
- Visualise cohort retention trends:
  - Early cohorts show higher long-term retention.
  - Recent cohorts (e.g. month-to-month) show declining retention.

---

## 3. Funnel Analysis

Constructed a user funnel from signup to active status:

1. **Signed Up** – All customers  
2. **Has Internet Service** – `InternetService != "No"`  
3. **Uses Streaming Services** – `StreamingTV` or `StreamingMovies = "Yes"`  
4. **Still Active** – `Churn = No`

**Conversion Rates**:
- Internet Service: ~78.3%
- Streaming Use: ~49.7%
- Still Active: ~73.5%

---

## 4. Simulated A/B Test

- Selected only **Month-to-Month** contract users.
- Randomly assigned to **Group A (Control)** or **Group B (Treatment)**.
- Simulated a retention campaign in Group B (set churn to 0 for demo).
- Used **Two-sample z-test** to test for significant difference in churn rates.

  Result:
  - z-statistic = 32.439
  - p-value < 0.0001
  - Statistically significant difference in churn

---

## 5. Churn Prediction Model

### Logistic Regression
- Features: `SeniorCitizen`, `tenure`, `MonthlyCharges`
- ROC AUC: **0.84**
- Precision: 83% (No churn), 69% (Churn)

### Random Forest + SMOTE (for imbalance)
- Balanced classes using SMOTE
- ROC AUC: **0.75**
- Accuracy: **68%**
- Recall (Churn class): 65%

Plotted ROC Curve, Precision-Recall Curve, and Confusion Matrix.

---

## Tools & Libraries

- `pandas`, `numpy`, `matplotlib`, `seaborn`
- `sklearn` (Logistic Regression, Random Forest, metrics)
- `imblearn` (SMOTE for class balancing)
- `statsmodels` (z-test for A/B testing)

---

## Takeaways

- **Contract Type** is a strong predictor of churn.
- **Retention rates** sharply drop for recent cohorts.
- **Streaming use** is common among retained users.
- Simple models with tenure and charges can provide meaningful churn predictions.
- Retention strategies can be evaluated via simulations and A/B tests.

---

## Next Steps

- Enhance feature engineering (e.g. customer service call counts).
- Deploy model into a **Streamlit dashboard**.
- Track **customer lifetime value (CLV)** and integrate with churn risk.
- Run **live experiments** using online A/B testing frameworks.

---

