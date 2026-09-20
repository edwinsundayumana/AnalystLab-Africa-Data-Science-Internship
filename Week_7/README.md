# HealthConnect Experience Lab — Data Science Track

**Current stage:** Week 7 — Testing, Refinement & End-to-End Validation

## Project Overview

HealthConnect Clinic is a fictional healthcare provider seeking to reduce missed appointments and make better use of appointment slots. This repository contains the Data Science track's contribution: predicting whether a patient will attend or miss (no-show) their appointment.


## Week 6 → Week 7 Progress

| | Week 6 | Week 7 |
|---|---|---|
| Validation approach | Single train/test split only | 5-fold cross-validation added |
| Overfitting check | Not done | Done — mild gap identified (0.0571) |
| Segment testing | Not done | Done — Recall/Precision checked across age group, appointment type, day |
| Feature set | 34 features (`gender_Prefer not to say` retained but flagged) | 33 features — `gender_Prefer not to say` removed and validated via ablation test |
| Threshold validation | Recommended on a single split | Tested on an independent second split — reframed as a range, not a fixed value |
| Cross-track activity | Findings shared with Data Analytics (integration only) | Full Test → Finding → Action cycle completed with Data Analytics (see below) |

## Week 7 Testing Results

**Final candidate model: Random Forest (tuned), 33 features (refined)**

| Test | Result |
|---|---|
| 5-fold cross-validation | ROC-AUC 0.6771 ± 0.0090 — confirms Week 6's result was not a lucky split |
| Train vs test gap | Train ROC-AUC 0.7240 vs Test 0.6669 (gap 0.0571) — mild overfitting identified |
| Segment performance (Recall) | 0.608 (Specialist Consultation) to 0.737 (age 55-64) — real inconsistency found |
| Segment performance (Precision) | 0.541 (Sunday) to 0.774 (Monday) |
| Feature ablation (`gender_Prefer not to say` removed) | ROC-AUC unchanged (0.6669→0.6668); Recall improved (0.6639→0.6742) — **feature removed** |
| Threshold (0.391) on independent split | Recall 0.887 → 0.83 — direction held, magnitude shifted; now framed as a ~0.83–0.89 recall range |

**Refined model performance:** Accuracy 0.6213 | Recall 0.6742 | ROC-AUC 0.6668

## Key Findings

- Cross-validation confirmed the Week 6 model generalises — its reported performance wasn't a single-split fluke.
- The model has a specific, operationally important blind spot: it is weakest exactly on **Specialist Consultation appointments** (Recall 0.608) — the costliest slots for the clinic to leave unfilled.
- Sunday appointments generate the most false alarms (Precision 0.541).
- `gender_Prefer not to say` was confirmed safe to remove — dropping it slightly improved recall.
- The 0.391 threshold is directionally reliable but should be communicated as an operating region (~0.83–0.89 recall), not an exact promised figure.
- Cross-track testing with Data Analytics independently confirmed three existing modelling decisions (feature set, `waiting_time_minutes` leakage exclusion, binary target definition) via their chi-square analysis, and surfaced a new candidate feature: patients with 2+ prior no-shows **and** 25.8km+ distance reach an 80% no-show rate (n=20) — logged for Week 8 testing.

## Limitations (Updated)

- Mild overfitting (train/test ROC-AUC gap 0.0571) — unresolved, flagged for Week 8 regularisation.
- Segment inconsistency (Specialist Consultation, Sunday) — unresolved, flagged as a Week 8 priority.
- Threshold behaviour varies by several points across data splits — treat 0.391 as approximate.
- Dataset remains synthetic; the ~51% no-show rate is far higher than a real clinic would see.
- Binned engineered features (`booking_lead_category`, `is_long_distance`) still underperform their raw continuous counterparts.
- `distance_to_clinic_km` (median-imputed) is the #2 most important feature — imputation noise remains unmeasured.

## Cross-Track Testing (Week 7)

Completed a full **Test → Finding → Action** cycle with the **Data Analytics** track (see `HealthConnect_Week7_CrossTrack_Testing_Evidence.docx` and `HealthConnect_Week7_DataScience_Collaborator_QA.docx`):
- **Received:** chi-square-validated findings on `previous_no_shows`, `distance_to_clinic_km`, their combined interaction, the `waiting_time_minutes` leakage issue, and a ruled-out age × appointment-type interaction.
- **Provided:** the model's segment performance table and refined feature list.
- **Outcome:** three existing decisions confirmed independently; one new feature candidate logged for Week 8; one previously-considered feature explicitly ruled out.
- **Still open:** a reciprocal question on whether Data Analytics' findings corroborate the Specialist Consultation/Sunday segment weaknesses — reply pending.

## Week 8 Priorities

1. Investigate why Specialist Consultation and Sunday appointments underperform.
2. Test the previous_no_shows × distance interaction feature identified via cross-track testing.
3. Apply mild additional regularisation (e.g. `min_samples_leaf=4`) to address the overfitting gap.
4. Confirm the refined 33-feature schema with ML Engineering — handoff not yet formally completed.
5. Get sign-off from Project Management/Data Analytics on the final operating threshold within the 0.83–0.89 recall range.
6. Close the loop on the pending Data Analytics reply regarding weak segments.

