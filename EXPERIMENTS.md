# Experimental Configurations

This document describes the experimental configurations implemented in the main Jupyter notebook.

## A0 – Raw-Merge Baseline
Baseline experiment using the raw merged feature representation without additional deduplication, Isolation Forest filtering, or SMOTE.

## A1 – Baseline Features
Evaluation using the baseline learner-level temporal feature representation (18 features).

## A2 – Proposed Features
Evaluation using the proposed enhanced feature representation (26 features).

## A3 – Proposed Features with Isolation Forest
Evaluation using the proposed feature representation combined with Isolation Forest-based anomaly screening.

## A4 – Proposed Features with SMOTE
Evaluation using the proposed feature representation with SMOTE-based class balancing.

## A5 – Proposed Features with Isolation Forest and SMOTE
Evaluation combining Isolation Forest-based anomaly screening and SMOTE-based class balancing.

## Evaluation Protocol

The notebook contains the experimental procedures and evaluation metrics. Please refer to the implementation for the exact data splits, model parameters, threshold-selection procedure, and preprocessing steps.

## Reproducibility

The experiments are implemented in the notebook:

`JCOMSS_OULAD_Experiments (3).ipynb`

The OULAD dataset must be downloaded separately from its official source.
