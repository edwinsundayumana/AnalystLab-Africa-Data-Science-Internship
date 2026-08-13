# Loan Prediction Datasets

This folder contains the datasets used in the **Week 2 Assignment** (Feature Engineering & Data Preprocessing for Machine Learning).

## 📁 File Descriptions

| File | Type | Description |
|------|------|-------------|
| `train_u6lujuX_CVtuZ9i.csv` | **Raw Dataset** | The original Loan Prediction training dataset from Kaggle (614 rows × 13 columns). Contains missing values, outliers, and mixed data types. |
| `cleaned_loan_data.csv` | **Cleaned Dataset** | The dataset after handling missing values, removing duplicates, correcting data types, capping outliers (IQR method), encoding categorical variables, and adding engineered features (`TotalIncome`, `Loan_to_Income_Ratio`, `EMI`). |
| `ml_ready_loan_data.csv` | **ML-Ready Dataset** | The final dataset after feature selection (removing redundant features) and scaling with **StandardScaler**. Ready to be fed directly into a classification model. |

## 🔄 Data Pipeline Flow

```text
Raw Data → Cleaning & Feature Engineering → Cleaned Dataset → Feature Selection & Scaling → ML-Ready Dataset