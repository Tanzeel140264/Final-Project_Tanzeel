**1. Project Overview: **
In this project, we have designed a three-step pipeline of Machine Learning to predict DL throughput for 5G networks along with anomaly detection.
By using a Hurdle Model architecture, the system accurately handles "zero-inflated" data (idle states) while maintaining high regression accuracy for active transmissions 

**2. PIPELINE ARCHITECTURE: **
The system operates through three specialized stages:
Stage 1: Scheduling Gate – A binary classifier (Random Forest/XGBoost) that distinguishes between scheduled (THP > 0) and unscheduled (THP = 0) states.
Stage 2: Throughput Regressor – A tuned regression model that estimates the exact throughput for active users.
Stage 3: Anomaly Classifier – A diagnostic tool that flags UEs in the bottom 10th percentile of performance (Anomalies).

**3. CORE TECHNICAL COMPONENTS: **
Algorithms: Comparative analysis between Random Forest, XGBoost, and LightGBM.
Feature Engineering: 19 features including Effective Resource (PRBs × (1-BLER)), SINR, and Distance.
Optimization: Sequential RandomizedSearchCV and GridSearchCV for hyperparameter tuning.
Imbalance Handling: Implementation of SMOTE to ensure minority "Anomaly" classes are detected accurately.

**4. FINAL RESULTS SUMMARY: **
Stage                 Best Performing Model           Key-Metric     Result
Stage 1               (Gating),Random Forest          Gate AUC,      1.0000
Stage 2               (Active),XGBoost                Regressor R²   0.4169
Combined Pipeline     XGBoost                         Full-Pop R²    0.5095
Stage 3               (Anomaly),XGBoost               ROC-AUC        0.9674

**5. DIRECTORY STRUCTURE: **
/outputs/eda/: Statistical reports, correlation heatmaps, and hypothesis test results.
/outputs/plots/: ROC curves, Actual vs. Predicted charts, and Feature Importance.
/outputs/models/: Serialized .pkl files of the best-performing tuned models.
master_5g_dataset.csv: The final preprocessed dataset used for modeling.

**6. KEY FINDINGS: **
Resource Dominance: Throughput is primarily driven by Resource Block (PRB) allocation (rho = 0.939) rather than signal quality (SINR) in this environment.
