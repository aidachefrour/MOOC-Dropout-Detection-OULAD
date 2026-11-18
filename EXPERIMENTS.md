# Experimental Configurations and Evaluation Protocol

## 1. Dataset Acquisition and Preparation

The experiments use the Open University Learning Analytics Dataset (OULAD).

The dataset preparation process includes:
- Dataset upload and extraction.
- Initial inspection of CSV files.
- Examination of column names and data types.
- Missing-value assessment.
- Dataset path verification.

## 2. Day-28 Prediction Cohort Definition

A prediction cohort is constructed using day 28 as the prediction cutoff.

The cohort construction procedure includes:
- Merging student information and registration records.
- Investigating withdrawal dates and inconsistent records.
- Excluding students registered after the prediction cutoff.
- Excluding students who withdrew on or before day 28.
- Excluding cases with unknown withdrawal timing.
- Defining the binary target variable:
  - 1: Eventual withdrawal.
  - 0: Other final outcomes.

## 3. Data Quality Audit

The data quality assessment examines:
- Missing values.
- Exact duplicate records.
- Learner coverage.
- Interaction records.
- Consistency between student and course identifiers.

## 4. Canonical Student–VLE Interaction Construction

Student–VLE interactions are processed to obtain a canonical representation of learner activity.

The processing stage investigates:
- Duplicate interaction records.
- Learner–resource–day aggregation.
- Click-count consistency.
- Temporal restrictions.

## 5. Student–Course Activity Validation

Student activity is checked against the prediction cohort and course information.

The validation process examines:
- Student and course matching.
- Learner coverage.
- Prediction-window consistency.
- Activity records within the observation period.

## 6. Behavioral Feature Engineering

Two feature representations are considered:

- **Baseline representation:** 18 features.
- **Proposed representation:** 26 features.

Feature matrices are constructed for subsequent experimental evaluation.

## 7. Experimental Evaluation Protocol

The experimental evaluation uses group-based cross-validation to account for learner-level grouping.

The implementation details, including model configurations, preprocessing operations, and evaluation settings, are provided in the experimental notebook.

## 8. Baseline and Ablation Experiments

The experimental framework considers six configurations:

- A0: Initial baseline experiment.
- A1: Baseline configuration.
- A2: Proposed feature representation.
- A3: Proposed features with Isolation Forest.
- A4: Proposed features with SMOTE.
- A5: Proposed features with Isolation Forest and SMOTE.

The exact implementation of each configuration is documented in the notebook.

## 9. Performance Evaluation

The experiments report the following metrics:

- Precision
- Recall
- F1-score
- Balanced Accuracy
- ROC-AUC
- PR-AUC

Fold-level results and aggregated statistics are used to examine model performance.

## 10. Reproducibility

The experimental notebook provides the data preparation procedures, feature construction steps, model evaluation code, and result-generation process.

The `requirements.txt` file specifies the Python dependencies required to reproduce the experiments.

Dataset source:

https://analyse.kmi.open.ac.uk/open-dataset
