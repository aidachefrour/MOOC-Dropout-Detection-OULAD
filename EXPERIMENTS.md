
# Experimental Configurations and Evaluation Protocol

## 1. Overview

This repository provides the experimental configurations used to investigate the impact of event-based data preprocessing, temporal feature engineering, and data-quality handling on MOOC dropout prediction using the Open University Learning Analytics Dataset (OULAD).

All experiments are implemented in the notebook:

`JCOMSS_OULAD_Experiments (3).ipynb`

The experiments are designed to compare alternative feature representations and assess the effects of outlier screening and class-imbalance handling.

## 2. Experimental Configurations

Six configurations (A0–A5) are considered.

| Configuration | Description | Feature Set |
|---|---|---|
| A0 | Raw merged data baseline | 18 features |
| A1 | Baseline feature representation | 18 features |
| A2 | Proposed enhanced feature representation | 26 features |
| A3 | Proposed features with Isolation Forest | 26 features |
| A4 | Proposed features with SMOTE | 26 features |
| A5 | Proposed features with Isolation Forest and SMOTE | 26 features |

### A0 – Raw Merged Data

This configuration evaluates the baseline data representation obtained after merging the relevant OULAD tables, without applying the proposed feature-engineering enhancements.

### A1 – Baseline Feature Representation

This configuration uses the baseline set of 18 learner-level features to establish a reference for comparison.

### A2 – Proposed Feature Representation

This configuration evaluates the proposed 26-feature representation, incorporating additional behavioral and temporal indicators derived from learner interaction records.

### A3 – Proposed Features with Isolation Forest

This configuration investigates the effect of Isolation Forest-based outlier screening on the proposed feature representation. The contamination parameter is set to 0.02.

### A4 – Proposed Features with SMOTE

This configuration applies the Synthetic Minority Over-sampling Technique (SMOTE) to the training data to investigate the effect of class-imbalance handling.

### A5 – Proposed Features with Isolation Forest and SMOTE

This configuration combines Isolation Forest-based outlier screening and SMOTE to evaluate their joint effect on the proposed feature representation.

## 3. Evaluation Protocol

The experiments use a group-aware cross-validation strategy to reduce the risk of learner-level information leakage between training and validation partitions.

The evaluation implementation uses:

- StratifiedGroupKFold for group-aware data partitioning.
- Student identifiers (`id_student`) as grouping information.
- Five outer folds for model evaluation.
- Four inner folds for hyperparameter and decision-threshold selection in the nested evaluation configurations.
- A fixed random seed of 42 to support reproducibility.

The nested evaluation procedure separates model selection from final performance estimation. Threshold selection is performed using the inner validation process rather than the outer test fold.

## 4. Classification Model

Random Forest is used as the principal classification algorithm.

The implementation includes median-value imputation for missing numerical feature values. Model parameters and preprocessing operations are specified in the corresponding notebook cells.

The evaluation reports the following performance measures:

- Precision
- Recall
- F1-score
- Balanced Accuracy
- Receiver Operating Characteristic Area Under the Curve (ROC-AUC)
- Precision–Recall Area Under the Curve (PR-AUC)

Execution time is also recorded to assess computational cost.

## 5. Outlier Detection

Isolation Forest is used to identify potentially anomalous learner interaction profiles.

The principal configuration uses:

- Number of estimators: 100
- Contamination: 0.02
- Random state: 42

Outlier detection is applied to the training partition in the corresponding cross-validation configurations. Validation and test observations are not removed through this training-stage filtering procedure.

Anomaly detection is treated as a screening operation. An anomalous interaction profile does not necessarily indicate incorrect data or academic failure.

## 6. Class-Imbalance Handling

SMOTE is investigated in configurations A4 and A5.

To prevent information leakage, oversampling is restricted to the training data within each evaluation fold. Validation and test partitions retain their original class distributions.

## 7. Reproducibility

The experiments are implemented in the Jupyter notebook:

`JCOMSS_OULAD_Experiments (3).ipynb`

The notebook contains the data preparation steps, feature construction, experimental configurations, model evaluation, and result generation.

The dependency list is provided in:

`requirements.txt`

The OULAD dataset is publicly available from the Open University Learning Analytics dataset repository:

https://analyse.kmi.open.ac.uk/open-dataset

Users should download the dataset separately and place the extracted files in the data directory expected by the notebook.

## 8. Notes on Result Interpretation

The experimental configurations are intended to provide a controlled comparison of alternative preprocessing and feature-engineering choices.

Performance differences should be interpreted alongside the class distribution, threshold-selection procedure, and cross-validation design. In particular, improvements in recall should not be considered independently of precision, F1-score, and PR-AUC.

The numerical results reported in the manuscript should be generated from, and checked against, the corresponding experiment outputs in the notebook.
