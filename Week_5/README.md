# Week 5 – HealthConnect No-Show Prediction: Baseline Model Development

## Overview
In Week 5, I moved my HealthConnect no-show prediction project from planning (Week 4) into practical implementation: data preparation, feature engineering, a train/test strategy, and a first baseline classification model.

## Completed task
1. **Week 4 review:** Confirmed the prediction problem (predict appointment no-shows), the binary target definition, and my Week 4 decision to exclude cancellations.
2. **Data preparation:** Inspected and cleaned the appointment data — handled missing values in `distance_to_clinic_km`, checked duplicates and data types, dropped the `patient_id` identifier, and excluded `waiting_time_minutes` due to leakage risk (it is only meaningful for attended appointments).
3. **Feature engineering:** Created a historical no-show ratio, a weekend appointment flag, and booking lead-time bands, each documented with its expected modelling value.
4. **Train/test strategy:** Stratified 80/20 split to preserve the class balance of the outcome.
5. **Baseline model:** Logistic Regression, chosen for interpretability and as a reliable reference point.
6. **Initial evaluation:** The baseline scored 46.0% accuracy on the three-outcome task (vs 44.9% for a dummy baseline) with ROC-AUC ≈ 0.63 — confirming the task is challenging and giving me a clear bar to beat.

## Key Decisions
- I kept cancellations out of the binary target after my evaluation confirmed they behave differently from no-shows.
- I excluded `waiting_time_minutes` to avoid leakage.
- I documented all limitations and my Week 6 improvement plan in the notebook.

## Contents
- `HealthConnect_Baseline_Model.ipynb`
- `data/healthconnect_cleaned.csv` (processed data — original file untouched)

## Next (Week 6)
Advanced models, hyperparameter tuning, class-imbalance handling, and deeper evaluation.

#AnalystLabAfrica