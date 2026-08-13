# Employee Attrition Analysis – ABC Manufacturing Ltd

## Project Overview
This project is part of the **Week 1 Assignment** of the **AnalystLab Africa Data Science Internship Programme**. As a Junior Data Scientist at AnalystLab Africa Consulting, I was engaged by **ABC Manufacturing Ltd** to investigate employee attrition. The HR department wants to understand why employees are leaving before investing in predictive machine learning models.

## Business Problem
ABC Manufacturing Ltd is experiencing employee turnover. The goal of this project is to perform an initial exploratory data analysis on historical HR data to understand the workforce and identify key factors contributing to attrition.

## Business Questions
1. What does the company's workforce look like?
2. Which departments have the highest employee attrition?
3. Does age influence attrition?
4. Does monthly income affect retention?
5. Does overtime influence attrition?
6. Which job roles experience the highest turnover?
7. Which variables appear important for future predictive modelling?

## Dataset
- **Source:** [IBM HR Analytics – Employee Attrition & Performance (Kaggle)](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset)
- **Size:** 1,470 employee records × 35 features
- **Target Variable:** Attrition (Yes / No)

## Tools Used
- Python (Google Colab)
- Pandas & NumPy (data manipulation)
- Matplotlib & Seaborn (visualisation)
- Git & GitHub (version control)

## Key Insights
- **Overall attrition rate is 16.1%** (237 out of 1,470 employees left).
- **Overtime is the strongest driver:** ~30.5% of overtime workers left vs ~10.4% of non-overtime workers.
- **Sales department** has the highest attrition rate (~20.6%) vs R&D (~13.8%).
- **Younger employees** are more likely to leave (leavers' median age ~30 vs ~36 for stayers).
- **Lower monthly income** correlates with attrition (leavers' median < $3,000 vs ~$5,000 for stayers).
- **Laboratory Technicians, Sales Executives and Sales Representatives** record the highest turnover.
- **Key variables for future modelling:** OverTime, Age, MonthlyIncome, Department, JobRole, BusinessTravel.
