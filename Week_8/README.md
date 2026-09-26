# HealthConnect Experience Lab — Data Science Track

**Programme:** AnalystLab Africa Experience Lab
**Project:** Improving Patient Appointment Attendance and Healthcare Support Using Data and AI
**Track:** Data Science
**Current stage:** Week 8 — Final Integration, Presentation & Project Showcase (project complete)

## Project Overview

HealthConnect Clinic is a fictional healthcare provider seeking to reduce missed appointments and make better use of appointment slots. This repository contains the Data Science track's contribution: predicting whether a patient will attend or miss (no-show) their appointment.



*(Earlier weeks' notebooks and documents remain in the repository as the evidence trail this package builds on — see the combined Week 6–8 README for the full history.)*

## Week 7 → Week 8: What Changed

The final candidate model is **unchanged** from Week 7 — Random Forest (tuned), 33 features. What Week 8 added was closure, not a new model:

| Open item at end of Week 7 | Resolved in Week 8 |
|---|---|
| Specialist Consultation / Sunday segment weakness — cause unknown | **Resolved:** Data Analytics statistically confirmed neither is a real pattern (p=0.50, p=0.24) — model instability on smaller subgroups, not a feature gap. Deprioritised. |
| `previous_no_shows × distance` interaction — flagged, untested | Logged as the agreed next test; not yet implemented (small sample, n=20, needs a dedicated test) |
| ML Engineering handoff — undocumented | **Resolved:** formal handoff package written (exact 33-feature schema, hyperparameters, threshold guidance) — documented and ready, though not yet confirmed received |
| No non-technical summary existed | Added, for stakeholders without a data science background |
| No final baseline-to-final comparison existed | Added — full Week 5→7 model progression in one table |

## Final Model Summary

**Random Forest (tuned), 33 features**
- `n_estimators=300, max_depth=5, min_samples_leaf=2, class_weight='balanced_subsample'`
- Cross-validated ROC-AUC: **0.6771 ± 0.0090**
- Recall (No-Show): **0.6742** at default threshold; **~0.83–0.89** at the recommended ~0.39 threshold
- Excludes: `waiting_time_minutes` (leakage, independently confirmed by Data Analytics) and `gender_Prefer not to say` (no predictive value, confirmed via ablation test)

## What the Model Can and Cannot Be Used For

**Ready for:** advisory flagging (prioritising reminder calls), overbooking safeguards on high-risk slots, a documented baseline for further iteration.

**Not ready for:** fully automated action (e.g. auto-cancelling a slot), Specialist Consultation scheduling specifically (weakest segment, highest cost to miss), or real deployment — all validation is on synthetic data (~51% no-show rate, far higher than a real clinic).

## Final Cross-Track Status

- **Data Analytics:** closed loop — findings exchanged, three modelling decisions independently confirmed, one feature ruled out, one new feature test queued. See `Reply_to_Dorothy_DataAnalytics.docx`.
- **ML Engineering:** handoff package documented and sent (Week 8 notebook, Part 6) — **not yet confirmed received**. This is the single most important open item before the model can be called fully integrated.
- **Project Management:** final modelling position reported in full — see `HealthConnect_Week8_DataScience_PM_Input.docx` and `Reply_to_PM_Week8_Input.docx`.

## Outstanding at Project Close

1. ML Engineering has not yet acknowledged or integrated the final handoff package.
2. The exact operating threshold (within the 0.83–0.89 recall range) still needs a business decision from Project Management/Data Analytics.
3. The `previous_no_shows × distance` interaction feature is agreed but not yet implemented or tested.
4. The mild overfitting gap (0.0571) remains unaddressed — a regularisation adjustment was identified but not attempted.
5. No validation has been performed on real (non-synthetic) clinic data at any stage of this project.

## Presentation

`HealthConnect_Week8_Final_Presentation.pptx` — 11 slides covering the problem, the Week 5→8 journey, model comparison, Week 7 testing results, the Data Analytics collaboration, the recall/precision trade-off, solution fit, and final limitations. Built to present alongside the required individual video walkthrough.

## How to Run

```bash
pip install pandas numpy scikit-learn matplotlib seaborn xgboost imbalanced-learn
jupyter notebook HealthConnect_Week8_Final_Model_DataScience_Package.ipynb
```

Requires `HealthConnect_Cleaned_Data.csv` (produced in Week 5) in the same directory. This notebook contains the full pipeline from Week 6/7 plus the Week 8 final documentation sections — it does not need to be run after an earlier notebook.
