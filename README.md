---
editor_options: 
  markdown: 
    wrap: 72
---

# Hospital Readmission Prediction

**Predicting 30-day hospital readmission risk using machine learning**

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3.0-orange)](https://scikit-learn.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

------------------------------------------------------------------------

## 📋 Project Overview

Hospital readmissions within 30 days of discharge are a critical
healthcare quality metric, costing the US healthcare system billions
annually. This project develops a machine learning solution to predict
patient readmission risk, enabling proactive interventions and improved
patient outcomes.

### Business Impact

-   **Cost Reduction**: Early readmission cost hospitals \~\$17.4B
    annually in Medicare penalties
-   **Patient Care**: Identifying high-risk patients enables targeted
    follow-up care
-   **Resource Optimization**: Better discharge planning and resource
    allocation
-   **Quality Metrics**: Improved hospital performance on CMS quality
    measures

## Problem Statement

**Objective**: Predict whether a diabetic patient will be readmitted to
the hospital within 30 days of discharge.

**Target Variable**: - **Class 0**: No readmission - **Class 1**:
Readmission after 30 days - **Class 2**: **High-risk** - Readmission
within 30 days (primary focus)

**Why this matters**: Early readmissions (\<30 days) indicate potential
gaps in care transition and are most preventable through intervention.

## Dataset

**Source**: [Diabetes 130-US Hospitals
(1999-2008)](https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008)

**Size**: 101,766 patient encounters across 130 US hospitals

**Features**: - **Demographics**: Age, gender, race - **Clinical**:
Diagnoses (ICD-9 codes), procedures, lab tests - **Medications**: 23
diabetes medication categories - **Utilization**: Prior
outpatient/inpatient/emergency visits - **Admission**: Type, source,
length of stay

**Key Challenge**: Significant class imbalance (minority class: early
readmission)

## Methodology

### 1. **Data Exploration** (`01_exploratory_data_analysis.ipynb`)

-   Comprehensive statistical analysis
-   Missing value assessment
-   Target variable distribution
-   Feature correlation analysis
-   Visualization of key patterns

### 2. **Data Preprocessing** (`02_data_preprocessing.ipynb`)

-   **Missing Value Treatment**: Dropped columns \>40% missing, imputed
    others
-   **Feature Engineering**:
    -   Grouped ICD-9 diagnosis codes into disease categories
    -   Created medication change indicators
    -   Built composite risk scores (utilization, comorbidity, treatment
        intensity)
-   **Encoding**: Ordinal (age), binary (gender), one-hot (diagnoses,
    race)
-   **Scaling**: StandardScaler for numerical features

### 3. **Model Training** (`03_model_training.ipynb`)

-   **Class Imbalance Handling**: SMOTE (Synthetic Minority
    Over-sampling Technique)
-   **Models Evaluated**:
    1.  Logistic Regression (baseline)
    2.  Decision Tree
    3.  Random Forest
    4.  Gradient Boosting
    5.  XGBoost
-   **Evaluation Metrics**: Accuracy, Precision, Recall, F1-Score,
    ROC-AUC

## Results

### Model Performance Comparison

| Model               | Accuracy   | Precision  | Recall     | F1-Score   | ROC-AUC    |
|------------|------------|------------|------------|------------|------------|
| **XGBoost**         | **0.6524** | **0.6389** | **0.6524** | **0.6427** | **0.7845** |
| Gradient Boosting   | 0.6489     | 0.6358     | 0.6489     | 0.6395     | 0.7823     |
| Random Forest       | 0.6401     | 0.6287     | 0.6401     | 0.6318     | 0.7756     |
| Logistic Regression | 0.6198     | 0.6124     | 0.6198     | 0.6145     | 0.7512     |
| Decision Tree       | 0.5987     | 0.5945     | 0.5987     | 0.5963     | 0.7234     |

###  Best Model: XGBoost

**Classification Report**:

```         
                          precision    recall  f1-score   support

         No Readmit         0.70      0.74      0.72      11,234
  Late Readmit (>30d)       0.58      0.53      0.55       4,567
 Early Readmit (<30d)       0.62      0.61      0.61       4,553

             accuracy                           0.65      20,354
            macro avg       0.63      0.63      0.63      20,354
         weighted avg       0.65      0.65      0.65      20,354
```

**Key Findings**: - Model achieves **65.2% overall accuracy** on unseen
data - **Early readmission detection** (Class 2): 61% recall -
identifies 6 out of 10 high-risk patients - **Feature importance**:
Prior utilization, number of medications, and diagnosis categories most
predictive - SMOTE significantly improved minority class performance

##  Key Insights

### Clinical Factors Driving Readmission

1.  **Prior Healthcare Utilization**: Patients with history of emergency
    visits/inpatient stays are at higher risk
2.  **Medication Complexity**: Higher number of medications correlates
    with readmission
3.  **Comorbidity Burden**: Multiple diagnoses increase risk
4.  **Diagnosis Categories**: Circulatory and respiratory conditions
    show elevated readmission rates
5.  **Age**: Elderly patients (70+) have distinct readmission patterns

### Model Interpretability

Top 5 Most Important Features: 1. `prior_utilization_score` (weighted
count of prior visits) 2. `num_medications` (medication count) 3.
`time_in_hospital` (length of current stay) 4. `number_inpatient` (prior
inpatient visits) 5. `diag_1_category_Circulatory` (primary diagnosis
category)

##  
