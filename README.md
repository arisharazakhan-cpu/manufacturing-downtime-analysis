# Manufacturing Downtime Analysis

## Project overview

This project analyzes manufacturing sensor and operational data to identify the primary drivers of machine downtime and to build a predictive model that estimates failure risk under real-world operating conditions.

The analysis is framed as a predictive maintenance problem, where failure events are rare but costly. The focus is therefore on ranking and early detection rather than raw classification accuracy.

The final output is an interpretable, end-to-end modeling pipeline that supports data-driven preventive maintenance decisions.

---

## Business context and motivation

Unplanned machine downtime is expensive, disruptive, and difficult to predict. In manufacturing environments, missing an impending failure is often far more costly than triggering a false alarm.

This project mirrors a real operational setting by:
• Working with severely imbalanced failure data
• Prioritizing recall over accuracy
• Explicitly tuning decision thresholds
• Emphasizing interpretability and actionability

The goal is not just prediction, but insight into *why* failures occur and *which signals* should be monitored in practice.

---

## Data description

The dataset follows a predictive maintenance structure and includes:
• Machine operating parameters
• Sensor measurements collected during operation
• Accumulated wear indicators
• Labeled failure events

The data includes both static attributes and dynamic operational signals, allowing comparison of their relative predictive importance.

---

## Quick start and reproducibility

Python 3.11 is recommended.

Clone the repository and navigate to the project root.

Create and activate a virtual environment
`python -m venv .venv`
`source .venv/bin/activate`

Install dependencies
`pip install -r requirements.txt`

Launch notebooks
`jupyter nbclassic`
or
`jupyter notebook`

All analysis can be reproduced by running the notebooks in numerical order.

---

## Exploratory analysis

Exploratory analysis focuses on data quality, feature distributions, and relationships between operating conditions and failure events.

Visual comparisons between failure and non-failure cases show clear separation in operational stress indicators such as rotational speed, torque, temperature differential, and tool wear. These observations inform feature selection and motivate the modeling strategy used downstream.

---

## Modeling approach

The failure prediction task exhibits extreme class imbalance, making accuracy an inappropriate primary metric.

Two models were evaluated:
• Logistic regression as a baseline
• Random forest for nonlinear modeling and feature interaction capture

Model performance was assessed using ROC AUC and average precision. Decision thresholds were tuned to prioritize recall, reflecting manufacturing environments where missed failures are significantly more costly than false positives.

The tuned random forest demonstrates strong ranking performance while maintaining high recall, making it suitable for early-warning preventive maintenance use cases.

---

## Feature importance and explainability

Permutation feature importance was used to evaluate which variables most strongly influence model performance.

The results show that failure risk is driven primarily by operational stress signals, including:
• Rotational speed
• Torque
• Temperature differential
• Accumulated tool wear

Static product attributes contribute minimally once operating conditions are accounted for. This indicates that *how* a machine is used matters more than *which product* it is producing.

![Random Forest Permutation Importance](reports/figures/rf_permutation_importance.png)

A ranked summary of these features is exported to:
`reports/data/random_forest_permutation_importance.csv`

---

## Results at a glance

| Model               | ROC AUC | Avg Precision | Recall (tuned) | Precision (tuned) |
| ------------------- | ------: | ------------: | -------------: | ----------------: |
| Logistic Regression |   0.882 |          0.39 |           0.86 |              0.11 |
| Random Forest       |   0.969 |         0.819 |           0.86 |              0.38 |

---

## Project structure

```
manufacturing-downtime-analysis/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   ├── 01_data_overview_quality_check.ipynb
│   ├── 02_baseline_failure_model.ipynb
│   └── 03_model_comparison_threshold_tuning.ipynb
│
├── outputs/
│   └── legacy_intermediate_files/
│
├── reports/
│   ├── figures/
│   │   └── rf_permutation_importance.png
│   └── data/
│       └── random_forest_permutation_importance.csv
│
├── src/
├── requirements.txt
├── README.md
└── .gitignore
```

---

## Key takeaways

Machine failure risk is driven primarily by operational stress rather than static product attributes.
Threshold tuning is essential when failure events are rare and recall is prioritized.
Explainable modeling techniques enable translation of predictions into actionable maintenance strategies.
Monitoring real-time operating conditions enables earlier intervention and reduced unplanned downtime.

---

## Data source

This project uses the AI4I 2020 Predictive Maintenance dataset. Dataset provenance and licensing information are available through the original publication and hosting source.
