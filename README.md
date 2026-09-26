# AnalystLab Africa – Data Science Internship Portfolio

This repository documents my weekly projects as a Data Science Intern at **AnalystLab Africa**. Each week I tackle a new business problem and apply the full data science workflow — from business understanding and data cleaning to feature engineering, visualisation, and machine learning.

## 📂 Projects

| Week | Project | Folder | Key Skills |
|------|---------|--------|------------|
| Week 1 | Employee Attrition Analysis (EDA) | [Week-1](./Week_1) | Pandas, EDA, Matplotlib/Seaborn, Business Insights |
| Week 2 | Loan Prediction – Feature Engineering & Preprocessing | [Week-2](./Week_2) | Data Cleaning, Encoding, Scaling, IQR Outlier Handling, Feature Selection |
| Week 3 | Loan Prediction – Advanced Analysis & Statistical Validation | [Week-3](./Week_3) | Advanced EDA, Hypothesis Testing (T-Test, Chi-Square, Mann-Whitney U, ANOVA), Feature Engineering, Feature Evaluation |
| Week 4 | HealthConnect No-Show Prediction (Problem Definition) | [Week-4](./Week_4) | ML Problem Framing, Target Variable Strategy, Data Leakage Risk Assessment, Binary Classification Planning |
| Week 5 | HealthConnect No-Show Prediction – Baseline Model | [week-5](./week_5) | Data Preparation, Feature Engineering, Train/Test Strategy, Logistic Regression Baseline, Initial Evaluation |


## 🧭 My Project Progression
- **Week 1:** I explored the IBM HR Attrition dataset and delivered my first business insights.
- **Week 2:** I worked on the Loan Prediction dataset and built a full preprocessing pipeline (cleaning, encoding, scaling, outlier treatment).
- **Week 3:** I validated my assumptions with statistical hypothesis testing, engineered advanced risk features, and refined my dataset for modelling.
- - **Week 4:** I joined the HealthConnect Clinic Experience Lab. I defined the machine learning problem for predicting patient no-shows, assessed the appointment dataset's quality and suitability, formulated my target variable strategy (filtering out cancellations and binarizing No-Show vs Attended), identified potential input features, and documented key modelling risks such as data leakage, class imbalance, and ethical bias.
- **Week 5:** I moved the HealthConnect no-show project into implementation — prepared the appointment data, engineered features (no-show ratio, weekend flag, lead-time bands), trained a logistic regression baseline on a stratified 80/20 split, and evaluated it (46.0% accuracy vs 44.9% dummy; ROC-AUC ≈ 0.63), documenting limitations and a Week 6 plan.
- **Week 6 (Next):** Model improvement — advanced models, tuning, class-imbalance handling, and deeper evaluation.

# HealthConnect Experience Lab — Data Science Track
## Full Project Arc: Week 6 → Week 8


## Project Overview

HealthConnect Clinic is a fictional healthcare provider seeking to reduce missed appointments and make better use of appointment slots. This repository documents the Data Science track's contribution across the project's integration, testing, and final stages: building, validating, and refining a model that predicts whether a patient will attend or miss (no-show) their appointment.

This README covers Weeks 6–8. Week 5 established the original baseline and is referenced throughout as the starting point.


## The Arc, Stage by Stage

### Week 5 — Baseline (starting point)
3-class Logistic Regression (Attended / No-Show / Cancelled). Result: ROC-AUC **0.628**, barely above a naive dummy classifier (0.499). The `Cancelled` class was essentially unpredictable (F1 = 0.12). This result was diagnostic, not a failure — it showed the 3-class formulation itself, not just the model, needed to change.

### Week 6 — Model Selection & Integration
Switched to a binary target (Attended vs. No-Show). Tested five configurations:

| Model | ROC-AUC | Recall |
|---|---|---|
| Logistic Regression | 0.6649 | 0.6536 |
| Random Forest (untuned) | 0.6375 | 0.6598 |
| XGBoost | 0.6333 | 0.6103 |
| **Random Forest (tuned)** | **0.6669** | **0.6639** |
| Random Forest (tuned + SMOTE) | 0.6662 | 0.6639 |

Random Forest (tuned) selected as the Week 6 candidate. SMOTE tested and dropped — classes were already close to balanced (51%/49%), so it added complexity with no benefit. First cross-track exchange completed with Data Analytics.

### Week 7 — Testing & Refinement
Stress-tested the Week 6 candidate rather than accepting it at face value:

| Test | Result |
|---|---|
| 5-fold cross-validation | ROC-AUC 0.6771 ± 0.0090 — confirmed stable, not a lucky split |
| Train vs. test gap | 0.0571 — mild overfitting identified |
| Segment performance | Recall 0.608–0.737 across appointment types; Precision 0.541–0.774 across days — real inconsistency found, worst on Specialist Consultation |
| Feature ablation | Removing `gender_Prefer not to say` improved Recall (0.6639→0.6742) with no ROC-AUC cost — **feature removed**, 33-feature model adopted |
| Threshold robustness | 0.391 threshold's direction held on an independent split, but exact recall shifted (0.887→0.83) — reframed as a range |

A full **Test → Finding → Action** cross-track cycle was completed with Data Analytics (Dorothy): findings exchanged, one feature ruled out, and the Specialist Consultation/Sunday segment question was raised (left open at the end of Week 7).

### Week 8 — Final Integration & Presentation
No new model was built — Week 8 closed out what Week 7 left open and packaged everything for handoff and presentation:

- **Data Analytics loop closed:** Specialist Consultation (p=0.50) and Sunday (p=0.24) statistically confirmed as *not* real patterns — model instability on smaller subgroups, not a fixable feature gap. A `previous_no_shows × distance` interaction feature (80% no-show rate, n=20) was agreed as the next test instead.
- **ML Engineering handoff formalised:** exact 33-feature schema, hyperparameters, and threshold guidance documented and sent — not yet confirmed received.
- **Final documentation completed:** baseline-vs-final comparison, consolidated error analysis, business suitability statement, non-technical stakeholder summary, and an honest "what this model can/cannot do" boundary.
- **Presentation built:** an 11-slide deck covering the full arc, for the required individual video and the group HC-POD walkthrough.

## Final Model

**Random Forest (tuned), 33 features**
```
n_estimators=300, max_depth=5, min_samples_leaf=2, class_weight='balanced_subsample', random_state=42
```
- Cross-validated ROC-AUC: **0.6771 ± 0.0090**
- Recall (No-Show): 0.6742 at default threshold; **~0.83–0.89** at the recommended ~0.39 threshold
- Excludes `waiting_time_minutes` (data leakage) and `gender_Prefer not to say` (no predictive value)

## What Changed Across the Whole Arc (Week 5 → Week 8)

| | Week 5 | Week 6 | Week 7 | Week 8 |
|---|---|---|---|---|
| Target | 3-class | Binary | Binary | Binary (unchanged) |
| Model | Logistic Regression | Random Forest (tuned) | Random Forest (tuned), refined | Same (unchanged) |
| Features | — | 34 | 33 | 33 (unchanged) |
| ROC-AUC | 0.628 | 0.6669 | 0.6771 (CV) | 0.6771 (unchanged, documented) |
| Validation | None | Single split | 5-fold CV + segment + ablation | Consolidated, handed off |
| Cross-track | — | Integration only | Full test-finding-action cycle | Loop closed + ML handoff |

## Honest Limitations at Project Close

- ML Engineering has not yet confirmed receipt or integration of the final model package.
- The exact operating threshold within the 0.83–0.89 recall range awaits business sign-off.
- A promising interaction feature (`previous_no_shows × distance`) is identified but not yet tested.
- A mild overfitting gap (0.0571) was found and documented but not corrected.
- Every result in this repository is based on synthetic data (~51% no-show rate); no real-clinic validation has occurred.


Requires `HealthConnect_Cleaned_Data.csv` (from Week 5) in the same directory. The Week 8 notebook is self-contained — it includes the full Week 6/7 pipeline plus final documentation, so it does not need to be run after the earlier notebooks. The Week 6 and Week 7 notebooks remain in this repository as the evidence trail for how each decision was reached.


## 👤 Author
**Edwin Sunday Umana** — Data Science Intern at AnalystLab Africa

*#AnalystLabAfrica*