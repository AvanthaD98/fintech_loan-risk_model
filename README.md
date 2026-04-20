# SBA Loan Default Predicting Model

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-blue?logo=github)](https://github.com/AvanthaD98/fintech_loan-risk_model)
[![Dataset](https://img.shields.io/badge/Data-SBA%20National-orange)](https://www.kaggle.com/datasets/mirbektoktogaraev/should-this-loan-be-approved-or-denied/data)
[![Dataset](https://img.shields.io/badge/Data-FRED%20Macrodata-green)](https://fred.stlouisfed.org/release/tables?rid=112&eid=1195039)

## 📌 Project Overview
This project develops a machine learning model to classify credit risk using historical U.S. Small Business Administration (SBA) loan data and state unemployment data. The model is designed to identify potential loan defaults at the point of approval and support better lending decisions by comparing a baseline Logistic Regression model with a tuned Random Forest model.

## 📊 Data Sources
1. **SBA National Dataset:** Historical records of 890k+ loans ([Source](https://www.kaggle.com/datasets/mirbektoktogaraev/should-this-loan-be-approved-or-denied/data)).
2.  **FRED Macroeconomic Data:** Monthly state-level unemployment rates matched to loan approval dates for temporal context ([Source](https://fred.stlouisfed.org/release/tables?rid=112&eid=1195039)).

---

## 🛠 Project Structure

### **Phase 1: Data Processing**
- **Sanitization:** Cleaned currency strings and mapped the `MIS_Status` target variable.
- **Leakage Prevention:** Removed variables not appropriate for approval-time prediction (for example `ChgOffPrinGr`, `BalanceGross`, and `DisbursementDate`).
- **Relational Merging:** Performed a time-aware merge with FRED data using state, year, and month.
- **Imputation & Outliers:** Applied median imputation for numeric data, constant imputation for categorical data, and **winsorization** to cap extreme values.

### **Phase 2: Exploratory Data Analysis (EDA)**
- Visualized target distributions and loan amount distributions.
- Generated a correlation heatmap to inspect relationships among numeric variables.
- Examined default patterns across business status and macroeconomic conditions.

### **Phase 3: Feature Engineering**
- **Feature Creation:** Developed `Guarantee_Percentage` to measure the share of the approved loan guaranteed by the SBA.
- **Normalization:** Applied one-hot encoding to categorical variables and `StandardScaler` to numeric variables.

### **Phase 4: Model Development & Evaluation**
- **Sampling:** Used a 50,000-row stratified sample to keep computation efficient while preserving the original class distribution.
- **Modeling:** Trained a baseline **Logistic Regression** model and a **Tuned Random Forest** model.
- **Optimization:** Used `GridSearchCV` with `StratifiedKFold` to optimize the Random Forest for **Recall**, since missing actual defaults is costly in credit risk.

### **Phase 5: Interpretation and Reporting**
- Discussed the main factors associated with default risk, including guarantee levels, loan size, unemployment conditions, and business maturity.
- Framed the model as a **Decision Support System** for underwriting triage and risk-based structuring.

---

## 📈 Model Performance

| Metric | Logistic Regression | **Tuned Random Forest** |
| :--- | :---: | :---: |
| **Accuracy** | 84.10% | **91.06%** |
| **Precision (Defaults)** | 63.15% | **79.43%** |
| **Recall (Defaults)** | 22.70% | **66.25%** |
| **F1 (Defaults)** | 33.40% | **72.24%** |
| **ROC AUC** | 0.8350 | **0.9375** |

---

## ▶️ Instructions to Run the Project
1. Clone the repository: `git clone https://github.com/AvanthaD98/fintech_loan-risk_model`
2. Ensure required libraries are installed: `pip install pandas numpy matplotlib seaborn scikit-learn`
3. Open `Fintech_Credit_Model_22189707_FIN5016.ipynb` and run all cells in order.

---

**Author:** Avantha Dilan Walakada Gamage |
**Student id:** 22189707 |
**Course:** Fintech & Blockchain Applications (FIN5016)
