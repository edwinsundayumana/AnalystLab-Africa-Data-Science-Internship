# HealthConnect Experience Lab 

**Project:** Improving Patient Appointment Attendance and Healthcare Support Using Data and AI
**Track:** Data Science
**Current stage:** Week 6 — Integration, Advanced Development & Validation

## Project Overview

HealthConnect Clinic is a fictional healthcare provider seeking to reduce missed appointments and make better use of appointment slots. This repository contains the Data Science track's contribution: predicting whether a patient will attend or miss (no-show) their appointment.


## Week 5 → Week 6 Progress

| | Week 5 | Week 6 |
|---|---|---|
| Target | 3-class (Attended / No-Show / Cancelled) | Binary (Attended / No-Show), validated approach |
| Model(s) | Logistic Regression only | Logistic Regression, Random Forest (untuned + tuned), XGBoost, Random Forest + SMOTE |
| Best result | ROC-AUC 0.628 | ROC-AUC 0.6669 (Random Forest, tuned) |
| Tuning | None | RandomizedSearchCV (Random Forest) |
| Class balancing | Not addressed | SMOTE tested — found unnecessary (classes already ~51/49) |
| Threshold | Default (0.5) | Optimised (0.391) — lifts No-Show recall from 0.66 → 0.887 |
| Error analysis | Not done | False positive / false negative breakdown completed |

## Week 6 Results Summary

**Final candidate model: Random Forest (tuned), without SMOTE**

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|
| **Random Forest (tuned)** | 0.6213 | 0.6216 | 0.6639 | 0.6421 | **0.6669** |
| Random Forest (tuned + SMOTE) | 0.6224 | 0.6228 | 0.6639 | 0.6427 | 0.6662 |
| Random Forest (untuned) | 0.6118 | 0.6119 | 0.6598 | 0.6349 | 0.6375 |
| Logistic Regression | 0.6108 | 0.6120 | 0.6536 | 0.6321 | 0.6649 |
| XGBoost (untuned) | 0.5886 | 0.5956 | 0.6103 | 0.6029 | 0.6333 |

**Top predictive features:** `booking_lead_days`, `distance_to_clinic_km`, `age`, `previous_appointments`, `appointment_load`, `no_show_rate`

**Recommended operating threshold:** 0.391 (rather than the default 0.5) if catching no-shows is prioritised over minimising false alarms — lifts No-Show recall to 0.887 at the cost of precision falling to 0.573. Final threshold choice pending sign-off from Project Management / Data Analytics on the relative cost of a false positive (extra reminder call) vs a false negative (a wasted clinic slot).

## Key Findings

- Switching to a binary target and tuning improved on the Week 5 baseline, but most of the model-family choice (Random Forest vs Logistic Regression) contributed only a small gain — careful threshold selection mattered more than model complexity.
- SMOTE added no measurable benefit since the classes were already close to balanced.
- False negatives (missed no-shows) were not concentrated among obviously low-risk patients, suggesting some no-show behaviour is close to the ceiling of what these features can predict.
- `gender_Prefer not to say` (a rare category flagged as an overfitting risk in Week 5) did not appear among the top 10 of 34 feature importances.

## Limitations

- Dataset is synthetic; the ~51% no-show rate is far higher than a real clinic would see — results are directional, not production-ready.
- Binned engineered features (`booking_lead_category`, `is_long_distance`) underperform their raw continuous counterparts in importance.
- `distance_to_clinic_km` (median-imputed) is the #2 most important feature, so imputation noise is an unmeasured source of uncertainty.
- XGBoost was evaluated with default-style hyperparameters, so the comparison with tuned Random Forest is not fully even.

## Cross-Track Integration

Collaborated with the **Data Analytics** track: shared the model's top feature ranking for them to check against their validated KPI findings on no-show rate by reminder channel and booking lead time. Full record in `HealthConnect_Week6_CrossTrack_Integration_Evidence.docx`.

## Week 7 Plan

1. Test the candidate model against unseen/held-out data.
2. Validate the 0.391 threshold against Data Analytics' slot-utilisation and no-show cost figures.
3. Revisit the binning approach for `booking_lead_category` and `is_long_distance`.
4. Re-run error analysis once real (non-synthetic) data is available.
5. Give XGBoost a full tuning pass before ruling it out.


Requires `HealthConnect_Cleaned_Data.csv` (produced in Week 5) in the same directory.
