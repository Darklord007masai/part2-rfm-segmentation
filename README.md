# Repository 2: Part 2 — Feature Engineering & Modeling Infrastructure

## Technical Architecture Overview
This component ingest features from the structured modeling table `rfm_modeling_snapshot.csv` to map behavioral markers to customer longevity.
* **Deterministic Splitting:** We rejected unseeded random cross-validation. Pre-defined segment identifiers (`train`, `validation`, and `test` data) were strictly isolated to enforce reproducibility and shield testing subsets from optimization bias.
* **Class Imbalance Realization:** Imbalanced distributions risk generating models biased toward accuracy while failing to detect true churn anomalies. This implementation coordinates penalizations utilizing an ensemble approach via class-weighted algorithms to increase minority-class target sensitivity.

## Technical Model Evaluation Results
*(Populate the values from the terminal display output after running the training script)*

* **Validation Accuracy:** [e.g., 81.4%]
* **Precision (Class 1 - Churn):** [e.g., 0.73] — Low Type I error protects retention budgets from waste.
* **Recall / Sensitivity (Class 1):** [e.g., 0.78] — Minimizing Type II errors avoids letting true high-risk churners slip away unnoted.
* **Receiver Operating Characteristic (ROC-AUC Value):** [e.g., 0.865]

## Explanations of Machine Learning Visualizations
*(Generated plots are accessible inside the evaluation_plots/ workspace directory)*

### 1. Confusion Matrix Diagnostic Matrix (`confusion_matrix.png`)
* Quantifies cross-classifications. In consumer retention mechanics, this acts similarly to a risk grid: tracking the raw rate of **False Positives (Type I errors)** where budget is wasted on healthy accounts, versus **False Negatives (Type II errors)** where customers churn silently without intervention.

### 2. Receiver Operating Characteristic Curves (`roc_curve.png`)
* Evaluates discriminative power across score thresholds. A high area under the curve (AUC) implies strong capacity to distinguish a satisfied subscriber from a consumer tracking toward account termination.

### 3. Feature Importance Map (`feature_importance.png`)
* Highlights internal behavior vectors forcing state transitions. Variables such as `recency_days`, high rates of `ticket_count_90d`, or changes in `sessions_30d` generally dominate variance metrics, proving that customer satisfaction data contains actionable warning signs.
