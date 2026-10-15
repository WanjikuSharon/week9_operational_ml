# MaishaWatch — Capstone Week 9 Progress Update

## Part C: Capstone Progress Check

**Project:** MaishaWatch Medical Equipment Predictive Maintenance System

## 1. Which ML algorithm did you choose and why?

For the first predictive-maintenance classification baseline, I chose the **Random Forest Classifier**.

I selected Random Forest because the MaishaWatch project uses structured tabular data containing operational, maintenance, degradation, utilization, risk, and sensor-related features. Random Forest is suitable because it can capture non-linear relationships and interactions between these variables without requiring those interactions to be manually defined.

It also provides **feature-importance values**, which will help explain which operational and maintenance factors contribute most to equipment risk.

The current repository has completed the data-engineering and feature-engineering stages and contains a processed equipment-level dataset with approximately **150 equipment records and 42 columns**. The model-training stage is the next major implementation step.

> **Current status note:** The reviewed repository does not yet contain a completed trained model artifact or final evaluation results. Therefore, Random Forest is the selected baseline algorithm for the next training stage rather than a model whose final performance has already been established.

---

## 2. How did you handle class imbalance?

Class imbalance is relevant in the current equipment-level dataset because positive events are less common than negative events.

The available labels include approximately:

- **Maintenance neglect:** 27 positive cases.
- **Usage discrepancy:** 42 positive cases.
- **Historical failure:** 27 positive cases.

To handle this imbalance, the planned ML training pipeline will:

1. Use **stratified train/test splitting** to preserve the proportion of positive and negative classes.
2. Use **class weighting**, such as `class_weight="balanced"` where supported, so minority-class events receive greater importance during training.
3. Evaluate the models using **precision, recall, F1-score, ROC-AUC, and confusion matrices** instead of relying mainly on accuracy.
4. Give particular attention to **recall** because missing a high-risk medical equipment failure can be operationally significant.
5. Consider controlled oversampling only if the baseline model performs poorly on the minority class.

This approach reduces the risk of producing a model that appears accurate simply because it predicts the majority "normal/no-risk" class while failing to identify critical equipment cases.

> **Current status note:** The repository does not yet contain completed training and evaluation outputs, so this is the documented imbalance-handling strategy for the upcoming baseline training stage.

---

## 3. What is one insight from your Feature Importance analysis that surprised you?

The current repository contains the completed feature-engineering pipeline and processed ML dataset, but it does **not yet contain a completed trained model or saved feature-importance analysis**. Therefore, a confirmed model-derived feature-importance ranking cannot honestly be reported yet.

One important insight that I expect to investigate during the feature-importance stage is whether **maintenance timing and recent risk trends are more influential than individual raw sensor readings**.

The engineered dataset includes features such as:

- `days_since_last_maintenance`
- `maintenance_overdue`
- `maintenance_event_count`
- `avg_downtime_hours`
- `avg_risk_score`
- `recent_risk_score`
- `risk_score_trend`
- `avg_degradation_index`
- Sensor anomaly indicators
- Critical operating-hour indicators

A potentially surprising result would be that a feature such as **risk_score_trend** or **days_since_last_maintenance** has greater predictive importance than a single temperature, vibration, pressure, or flow-rate measurement.

This would be operationally meaningful because it would suggest that equipment risk depends strongly on **how the equipment is changing over time and whether maintenance has kept pace with deterioration**, rather than on one abnormal sensor reading alone.

This insight will be confirmed or rejected after training the Random Forest baseline and generating the actual feature-importance ranking.

> **Current status note:** No final feature-importance result is yet present in the repository, so the final submission should not claim a specific model-derived ranking until training has been completed.

---

# Week 9 Capstone Summary

The MaishaWatch project has successfully completed:

- Multi-source medical equipment data preparation
- Sensor telemetry generation and processing
- Equipment metadata preparation
- Maintenance history preparation
- Failure-event preparation
- Usage-reporting feature preparation
- Feature engineering
- Equipment-level ML dataset preparation
- Creation of labels for maintenance neglect, usage discrepancy, and historical failure

The project is now transitioning from:

> **Machine Learning Dataset Preparation → Actual Model Training and Evaluation**

## Selected ML Direction

- **Baseline algorithm:** Random Forest Classifier
- **Reason:** Strong fit for structured, non-linear predictive-maintenance data and supports feature-importance analysis
- **Class imbalance strategy:** Stratified splitting, class weighting, and minority-class-focused evaluation
- **Feature importance:** To be generated after baseline training

## Next Steps

1. Create the ML model-training script.
2. Perform feature selection and data-leakage checks.
3. Create stratified training and testing datasets.
4. Train the Random Forest baseline.
5. Evaluate precision, recall, F1-score, ROC-AUC, and the confusion matrix.
6. Generate and analyze feature importance.
7. Compare the baseline model with another suitable algorithm if necessary.
8. Save the selected trained model for integration with the MaishaWatch backend and dashboard.

## Current Project Status

**Data Engineering and Feature Engineering: Completed**  
**ML Training Dataset: Prepared**  
**Baseline Model Selection: Completed**  
**Model Training, Evaluation, and Feature Importance Analysis: Next Stage**
