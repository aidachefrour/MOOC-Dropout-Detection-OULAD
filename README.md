# MOOC-Dropout-Detection-OULAD
# MOOC Dropout Detection Using Event-Based Learning Analytics

## Overview

This repository provides the source code accompanying the research study on preprocessing event-based learning analytics data for MOOC dropout detection using the Open University Learning Analytics Dataset (OULAD).

The project focuses on data quality assessment, temporal feature engineering, anomaly screening, class imbalance handling, and machine-learning-based dropout prediction.

## Dataset

The experiments use the publicly available Open University Learning Analytics Dataset (OULAD).

Dataset source: https://analyse.kmi.open.ac.uk/open-dataset

The original dataset is not redistributed in this repository. Users must download it from the official source and follow its terms of use.

## Methodology

The implementation covers the following stages:

1. Event-based data preprocessing and data-quality assessment.
2. Duplicate detection and handling.
3. Learner-level temporal feature extraction.
4. Baseline and proposed feature representations.
5. Isolation Forest-based anomaly screening.
6. SMOTE-based class imbalance handling.
7. Random Forest-based dropout prediction.
8. Cross-validation and performance evaluation.

## Experimental Configurations

The notebook includes the following experimental configurations:

- **A0:** Raw-merge baseline.
- **A1:** Baseline feature representation.
- **A2:** Proposed feature representation.
- **A3:** Proposed features with Isolation Forest.
- **A4:** Proposed features with SMOTE.
- **A5:** Proposed features with Isolation Forest and SMOTE.

Please refer to the notebook for the exact implementation and experimental settings.

## Repository Contents

- `JCOMSS_OULAD_Experiments (3).ipynb`: Main experimental notebook.

## Requirements

The experiments were developed using Python in Google Colab.

Install the required Python packages using:

pip install -r requirements.txt

The notebook uses NumPy, Pandas, Matplotlib, Scikit-learn, and imbalanced-learn.

The OULAD dataset must be downloaded separately from its official source.

## Reproducibility

The notebook documents the data-processing and experimental workflow. Reproducing the results requires the OULAD dataset and the corresponding experimental configuration.

## Code Availability

The source code is publicly available at:

https://github.com/aidachefrour/MOOC-Dropout-Detection-OULAD

## Citation

If you use this code, please cite the associated research article once its bibliographic information is available.

## License

A license will be specified by the repository authors.
