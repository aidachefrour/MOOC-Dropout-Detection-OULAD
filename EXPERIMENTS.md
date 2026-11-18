# Experimental Configurations and Reproducibility

## 1. Overview

This document describes the experimental configurations implemented in the main Jupyter notebook accompanying the study on preprocessing event-based learning analytics data for MOOC dropout detection using OULAD.

The experiments compare a raw-merge baseline, a baseline feature representation, and an enhanced feature representation, with additional configurations incorporating Isolation Forest and SMOTE.

## 2. Experimental Configurations

- **A0 – Raw-Merge Baseline:** Uses the raw merged feature representation without additional deduplication, Isolation Forest filtering, or SMOTE.
- **A1 – Baseline Features:** Uses the baseline learner-level temporal feature representation (18 features).
- **A2 – Proposed Features:** Uses the enhanced feature representation (26 features).
- **A3 – Proposed Features + Isolation Forest:** Applies Isolation Forest-based anomaly screening to the proposed features.
- **A4 – Proposed Features + SMOTE:** Applies SMOTE-based class balancing to the proposed features.
- **A5 – Proposed Features + Isolation Forest + SMOTE:** Combines Isolation Forest-based anomaly screening and SMOTE-based class balancing.

## 3. Evaluation Protocol

The A1–A5 ablation experiments use nested group-stratified cross-validation:

- Outer cross-validation: 5 folds.
- Inner cross-validation: 4 folds.
- Splitting strategy: StratifiedGroupKFold.
- Group identifier: `id_student`.
- Random state: 42.
- The same outer folds are used across A1–A5 to support consistent comparisons.

The A0 experiment is implemented separately using the same 5-fold outer and 4-fold inner group-stratified evaluation structure.

## 4. Model and Preprocessing Settings

### Random Forest

- Number of estimators: 200.
- Random state: 42.
- Class weight: None.
- Parallel processing: `n_jobs=-1`.

### Missing-Value Imputation

Median imputation is fitted on the training subset and subsequently applied to the corresponding validation or test subset.

### Isolation Forest

For A3 and A5:

- Number of estimators: 100.
- Contamination: 0.02.
- Random state: 42.
- Parallel processing: `n_jobs=-1`.

Anomaly detection is performed using training data only. Flagged observations are excluded from the corresponding training subset, while validation and test observations are retained.

### SMOTE

For A4 and A5:

- Random state: 42.
- Number of nearest neighbors: `min(5, minority_class_count - 1)`.
- Sampling strategy: default automatic balancing.

SMOTE is applied exclusively to the training subset.

## 5. Decision-Threshold Selection

The classification threshold is selected within the inner cross-validation procedure using out-of-fold training probabilities.

The threshold search range is 0.05–0.50, with an increment of 0.01. The selected threshold maximizes the F1-score on the inner out-of-fold predictions.

The selected threshold is then applied to the untouched outer test fold.

## 6. Recorded A1–A5 Results

The following values correspond to the saved experimental output in the main notebook.

| Configuration | Features | Precision | Recall | F1-score | ROC-AUC | PR-AUC | Runtime (s) |
|---|---:|---:|---:|---:|---:|---:|---:|
| A1 – Baseline | 18 | 0.1961 | 0.8288 | 0.3172 | 0.5553 | 0.2108 | 272.85 |
| A2 – Proposed | 26 | 0.1914 | 0.8615 | 0.3132 | 0.5498 | 0.2098 | 347.80 |
| A3 – Proposed + IF | 26 | 0.1911 | 0.8683 | 0.3133 | 0.5532 | 0.2107 | 349.11 |
| A4 – Proposed + SMOTE | 26 | 0.1899 | 0.8597 | 0.3111 | 0.5503 | 0.2087 | 626.79 |
| A5 – Proposed + IF + SMOTE | 26 | 0.1894 | 0.8771 | 0.3116 | 0.5489 | 0.2085 | 641.17 |

The metrics are calculated from the pooled outer-fold out-of-fold predictions. Runtime values are the recorded execution times from the notebook and may vary across hardware and execution environments.

## 7. Reproducibility

The main experimental notebook is:

`JCOMSS_OULAD_Experiments (3).ipynb`

The OULAD dataset must be downloaded separately from the official source:

https://analyse.kmi.open.ac.uk/open-dataset

Install the required Python packages using:

```bash
pip install -r requirements.txt
```

The notebook contains the preprocessing, feature-engineering, model-training, and evaluation procedures.

## 8. Code Availability

The source code is publicly available at:

https://github.com/aidachefrour/MOOC-Dropout-Detection-OULAD

## 9. Citation

Please cite the associated research article when using this implementation. Bibliographic details will be added after publication.
