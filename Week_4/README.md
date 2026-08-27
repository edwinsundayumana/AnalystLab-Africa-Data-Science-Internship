# Week 4: HealthConnect Project Kickoff & Problem Understanding (Experience Lab)

## Overview
This folder contains my Week 4 deliverables for the **AnalystLab Africa Data Science Internship**. The focus of this week's Experience Lab was to define the machine learning problem for HealthConnect Clinic, assess the available appointment data, and outline my initial modelling strategy to predict patient "No-Shows".

## What I Did This Week
1. **Problem Definition:** Framed the business problem of appointment non-attendance as a binary classification machine learning task.
2. **Target Variable Strategy:** Evaluated the `appointment_outcome` variable and made the strategic decision to filter out "Cancelled" appointments to focus purely on predicting passive "No-Shows" vs. "Attended" visits.
3. **Initial Data Assessment:** Loaded and inspected the HealthConnect dataset, identifying missing values, data types, and the baseline class imbalance.
4. **Feature Identification:** Categorized potential input features into Demographics, Logistics, Patient History, and Clinic Interventions.
5. **Risk & Limitation Analysis:** Identified critical modelling risks, including potential data leakage in the `waiting_time_minutes` variable and the ethical implications of demographic bias.