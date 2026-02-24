
# Cloover Data Science Case Study  
## Optimizing Credit Risk & Pricing for Renewable Energy Financing

---

## 📌 Overview

This project analyzes anonymized loan data from Cloover to:

1. Evaluate credit risk factors
2. Segment customers into risk tiers
3. Build a predictive model for default probability (PD)
4. Provide actionable pricing and risk management recommendations

The objective is to improve underwriting efficiency, risk differentiation, and loan pricing optimization.

---

## 📂 Project Structure

- `EDA.ipynb` → Full analysis notebook  
- `data/` → Input datasets (not included if confidential)  
- `figures/` → Exported charts used in analysis  
- `README.md` → Project documentation  

---

## 1️⃣ Data Exploration & Cleaning

### Key Steps
- Checked missing values and duplicates
- Identified outliers via boxplots
- Evaluated class imbalance (~3% default rate)
- Checked correlations and multicollinearity (VIF analysis)
- Engineered financial ratios (loan-to-income, debt-to-income, savings coverage)

### Summary Statistics
- Average loan amount: ~€24.8k  
- Average interest rate: ~5.5%  
- Loan tenor: Mostly 60–120 months  
- Default rate: ~3%

---

## 2️⃣ Risk Profiling

Customers were segmented into **Low / Medium / High risk** tiers using:

- `schufa_score`
- `loan_to_income_ratio`
- `debt_to_income`
- `loan_to_value`
- `savings_coverage_ratio`

### Key Findings

| Segment | Default Rate |
|----------|-------------|
| Low      | ~1–2% |
| Medium   | ~2–3% |
| High     | ~7–8% |

Strong risk dispersion exists.

However, interest rates vary only marginally across segments — suggesting limited risk-based pricing differentiation.

---

## 3️⃣ Predictive Modeling

### Model Used
Logistic Regression (primary model)

Features:
- schufa_score
- loan_to_income_ratio
- debt_to_income
- loan_to_value
- savings_coverage_ratio

### Performance Metrics

- **AUC:** ~0.84  
- **Cross-validated AUC:** ~0.85 (stable)  
- **KS Statistic:** ~0.64  

The model demonstrates strong discriminatory power for a retail credit portfolio.

### Feature Importance (Standardized Coefficients)

- Credit score is the dominant driver
- Higher debt burden increases default risk
- Affordability metrics provide incremental explanatory power

SHAP values were used to validate directional impact consistency.

---

## 4️⃣ Key Insights

- Clear risk differentiation exists (Low vs High default gap ≈ 4–5x)
- Credit quality is the primary structural driver
- Financial leverage significantly contributes to risk
- Pricing spreads show limited differentiation despite risk gaps

---

## 5️⃣ Strategic Recommendations

### 1. Implement PD-Linked Pricing
Move from flat spreads → Base Rate + Risk Premium tied to predicted PD.

### 2. Introduce Affordability Guardrails
Formalize thresholds for leverage metrics (DTI, loan-to-income) with mitigation actions.

### 3. Separate Origination & Behavioral Risk
Use the logistic model for origination scoring.
Develop behavioral monitoring rules for early delinquency detection.

### 4. Strengthen Model Governance
Clarify feature definitions (e.g., bureau vs post-origination variables) to prevent leakage and support scalability.

---

## 6️⃣ Deployment Considerations

Suggested stack for production integration:

- GCP / BigQuery for centralized data storage
- Scheduled model retraining via Cloud Scheduler
- Model API deployed via Cloud Run
- BI dashboards (Looker / Data Studio) for monitoring:
  - Default rate
  - PD distribution
  - Segment migration
  - Pricing vs realized loss

---

## ⚙️ Tech Stack

- Python (pandas, numpy)
- scikit-learn
- SHAP
- matplotlib / seaborn
- statsmodels (VIF)

---

## 📈 Business Impact

By aligning pricing with predicted default risk and strengthening affordability controls, Cloover can:

- Improve risk-adjusted returns
- Reduce underpricing of high-risk borrowers
- Scale underwriting more efficiently
- Enhance long-term portfolio stability

---

## Author

Abheendra
Data Science Candidate  
