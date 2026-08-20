# Week 3: Advanced Data Analysis, Statistical Validation & Feature Engineering (Loan Prediction)

## Overview
This folder contains my complete Week 3 work for the **AnalystLab Africa Data Science Internship**. Continuing from my Week 2 preprocessing of the Loan Prediction dataset, I performed advanced exploratory data analysis, validated my assumptions with statistical hypothesis testing, engineered new features, evaluated feature usefulness, and refined my dataset for Week 4 machine learning.

## What I Did This Week
1. **Project Continuity Review** – I summarised how my Week 3 analysis builds on Weeks 1 and 2.
2. **Advanced EDA** – I produced 12+ advanced visualisations (violin plots, boxplots, scatter plots, pairplots, correlation charts) to uncover deeper relationships.
3. **Statistical Hypothesis Testing** – I ran four tests (Welch's T-Test, Chi-Square, Mann-Whitney U, One-Way ANOVA) and interpreted every p-value in business terms.
4. **Advanced Feature Engineering** – I created `Income_Per_Dependent`, `Loan_Term_Category`, and `High_Risk_Flag`.
5. **Feature Evaluation & Selection** – I checked multicollinearity and target correlations to justify which features to keep or drop.
6. **Dataset Refinement** – I exported my final modelling dataset for Week 4.

## Tools & Libraries
Python (Google Colab) • Pandas • NumPy • Matplotlib • Seaborn • SciPy (stats) • Scikit-learn

## Key Insights I Discovered
- Credit history remains the strongest statistically validated predictor of loan approval (Chi-Square, p < 0.05).
- Financial burden (Loan-to-Income ratio) differs significantly between approved and rejected loans (Mann-Whitney U, p < 0.05).
- My engineered `High_Risk_Flag` cleanly separates high-risk applicants and will be a powerful feature in Week 4.
- Applicant incomes differ significantly across property areas (ANOVA, p < 0.05), supporting region-specific loan products.

*#AnalystLabAfrica*