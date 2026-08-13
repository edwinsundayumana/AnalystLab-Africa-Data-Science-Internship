# Week 2: Feature Engineering & Data Preprocessing for Machine Learning (Loan Prediction)

## Project Overview
This project is part of the **Week 2 Assignment** of the **AnalystLab Africa Data Science Internship Programme**. Building on the exploratory data analysis skills developed in Week 1, this week's focus is on transforming raw, messy business data into a high-quality, machine-learning-ready dataset. 

The project tackles the **Loan Prediction Problem**, where the goal is to prepare historical loan application data so that a predictive classification model can accurately determine whether a future loan should be approved or rejected.

## Business Problem
Financial institutions face a significant challenge in manually evaluating loan applications. Manual underwriting is time-consuming, prone to human bias, and carries the risk of approving high-risk applicants (leading to defaults) or rejecting creditworthy customers (leading to lost revenue). The objective of this project is to clean, transform, encode, scale, and engineer features from raw loan data to create a robust foundation for automated, data-driven credit risk assessment.

## Dataset
- **Source:** [Loan Prediction Dataset (Kaggle)](https://www.kaggle.com/datasets/altruistdelhite04/loan-prediction-problem-dataset)
- **Target Variable:** `Loan_Status` (Y = Approved, N = Rejected)
- **Key Challenges Handled:** Missing values across multiple columns, extreme outliers in income and loan amounts, mixed data types, and categorical variables requiring encoding.

## Tools & Libraries Used
- **Python** (Google Colab)
- **Pandas & NumPy** (Data manipulation, missing value imputation, feature engineering)
- **Matplotlib & Seaborn** (Outlier detection via boxplots, correlation heatmaps)
- **Scikit-Learn** (`StandardScaler` for feature scaling)

## Key Preprocessing & Feature Engineering Steps
1. **Missing Value Imputation:** Used Mode for categorical variables (e.g., `Gender`, `Married`) and Median for skewed numerical variables (e.g., `LoanAmount`).
2. **Outlier Treatment:** Applied the **IQR (Interquartile Range) method** to cap extreme outliers in `ApplicantIncome`, `CoapplicantIncome`, and `LoanAmount` rather than dropping valuable rows.
3. **Feature Engineering:** Created powerful new financial indicators:
   - `TotalIncome` (Applicant + Co-applicant income)
   - `Loan_to_Income_Ratio` (Measures financial burden)
   - `EMI` (Approximate monthly installment strain)
4. **Feature Encoding:** Applied Binary Mapping for Yes/No variables and **One-Hot Encoding** for nominal variables like `Property_Area`.
5. **Feature Scaling:** Applied **StandardScaler** to normalize numerical features, ensuring algorithms relying on distance metrics perform optimally.
6. **Feature Selection:** Removed redundant and highly correlated features (like original income columns) to prevent multicollinearity.
