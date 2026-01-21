# Manufacturing Downtime Analysis

## Project overview

**Goal:**
Analyze manufacturing sensor and operational data to identify key drivers of machine downtime and build a model that estimates failure risk under real-world operating conditions.

**Data:**
Predictive maintenance–style dataset containing machine operating parameters, sensor measurements, and labeled failure events.

**Outcome:**
An end-to-end analysis including exploratory data visualization, multiple predictive models, threshold tuning for failure detection, and actionable insights to support preventive maintenance decisions.

## Exploratory analysis

Initial analysis focuses on understanding data quality, feature distributions, and relationships between operating conditions and machine failures. Visualizations highlight how operational stress indicators such as tool wear, torque, rotational speed, and temperature differences differ between failure and non-failure cases.

This step establishes domain intuition and informs feature engineering decisions used in downstream modeling.

## Modeling and insights

This project builds a predictive maintenance pipeline to estimate machine failure risk under severe class imbalance. Multiple models were evaluated, including logistic regression and a random forest, with performance assessed using ROC AUC and average precision rather than accuracy alone.

Decision thresholds were explicitly tuned to prioritize recall, reflecting real manufacturing tradeoffs where missed failures are significantly more costly than false alarms. The tuned random forest demonstrates strong ranking performance while maintaining high recall for failure events, making it suitable for early-warning use cases in preventive maintenance.

Permutation feature importance reveals that failure risk is driven primarily by operational stress signals such as rotational speed, torque, temperature differential, and accumulated tool wear. Static product attributes contribute minimally once operating conditions are accounted for, indicating that how a machine is used matters more than which product type it belongs to.

A summary of the top predictive signals is exported to `outputs/random_forest_permutation_importance.csv` for downstream analysis and reporting. The full modeling workflow, including threshold tuning and explainability analysis, is documented in the model comparison notebook.
