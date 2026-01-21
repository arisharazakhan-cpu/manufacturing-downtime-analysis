
# Manufacturing Downtime Analysis

## Project overview

**Goal:**
Analyze manufacturing sensor and operational data to identify key drivers of machine downtime and build a model that estimates failure risk under real-world operating conditions.

**Data:**
Predictive maintenance–style dataset containing machine operating parameters, sensor measurements, and labeled failure events.

**Outcome:**
An end-to-end analysis including exploratory data visualization, multiple predictive models, threshold tuning for failure detection, and actionable insights to support preventive maintenance decisions.

---

## Getting started

Python 3.11 recommended.

1. Create and activate a virtual environment
   `python -m venv .venv`
   `source .venv/bin/activate`

2. Install dependencies
   `pip install -r requirements.txt`

3. Launch notebooks
   `jupyter nbclassic`
   or
   `jupyter notebook`

---

## Exploratory analysis

Initial analysis focuses on understanding data quality, feature distributions, and relationships between operating conditions and machine failures. Visualizations highlight how operational stress indicators such as tool wear, torque, rotational speed, and temperature differences differ between failure and non-failure cases.

This step establishes domain intuition and informs feature engineering decisions used in downstream modeling.

---

## Modeling and insights

This project builds a predictive maintenance pipeline to estimate machine failure risk under severe class imbalance. Multiple models were evaluated, including logistic regression and a random forest, with performance assessed using ROC AUC and average precision rather than accuracy alone.

Decision thresholds were explicitly tuned to prioritize recall, reflecting real manufacturing tradeoffs where missed failures are significantly more costly than false alarms. The tuned random forest demonstrates strong ranking performance while maintaining high recall for failure events, making it suitable for early-warning use cases in preventive maintenance.

Permutation feature importance reveals that failure risk is driven primarily by operational stress signals such as rotational speed, torque, temperature differential, and accumulated tool wear. Static product attributes contribute minimally once operating conditions are accounted for, indicating that how a machine is used matters more than which product type it belongs to.

A summary of the top predictive signals is exported to `outputs/random_forest_permutation_importance.csv` for downstream analysis and reporting. The full modeling workflow, including threshold tuning and explainability analysis, is documented in the model comparison notebook.

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
│   ├── raw/                # Original dataset
│   └── processed/          # Generated features (if applicable)
│
├── notebooks/
│   ├── 01_data_overview_quality_check.ipynb
│   ├── 02_baseline_failure_model.ipynb
│   └── 03_model_comparison_threshold_tuning.ipynb
│
├── outputs/
│   ├── random_forest_permutation_importance.csv
│   └── model_metrics_summary.csv
│
├── src/                    # Reusable code (optional extension)
├── requirements.txt
├── README.md
└── .gitignore
```

---

## Key takeaways

* Machine failure risk is driven primarily by **operational stress**, not static product attributes.
* **Threshold tuning** is critical in imbalanced failure prediction where recall is prioritized.
* Explainable models help translate predictive signals into **actionable maintenance decisions**.
* Monitoring real-time operating conditions can reduce unplanned downtime while managing inspection costs.

---

## Data source

This project uses the AI4I 2020 Predictive Maintenance dataset. Dataset provenance and licensing information are available through the original publication and hosting source.

