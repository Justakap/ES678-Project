# Bank Marketing Leakage Audit

Investigates target leakage and model evaluation issues in the UCI Bank Marketing dataset (`bank-additional-full.csv`), notably the `duration` feature which is only known after a call outcome is determined.

## Structure

- `data/` — raw dataset (`bank-additional-full.csv`)
- `notebooks/` — exploratory and analysis notebooks
- `src/` — reusable code (data loading, preprocessing, modeling utilities)
- `results/` — generated figures, metrics, model outputs
- `paper/` — writeup / report

## Data source

UCI Machine Learning Repository — Bank Marketing dataset (`bank-additional-full.csv`, the full version with all examples and 20 inputs).
