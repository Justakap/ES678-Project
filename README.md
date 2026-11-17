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
Citation: Moro, S., Rita, P., Cortez, P. (2012). Bank Marketing [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5K306.
The dataset is public and released under the UCI repository's CC BY 4.0 terms, so the full file is included at `data/bank-additional-full.csv` in this repository — no separate download step is required.

## Code repository

https://github.com/Justakap/ES678-Project

## Reproducing results

1. Clone the repository: `git clone https://github.com/Justakap/ES678-Project.git`
2. Create an environment with `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `joblib`, and `jupyter`.
3. Run the notebooks in order, `01` through `09` (`notebooks/01_data_understanding.ipynb` … `notebooks/09_final_test_evaluation.ipynb`). Each notebook reads only from `data/` and `results/` produced by earlier notebooks; the test set (`results/final/`) is read exactly once, by notebook `09`.
4. `results/models/*random_forest*.joblib` are excluded from version control (30–77MB each). Regenerate them by rerunning notebooks `05_model_development.ipynb` and `06_leakage_experiment.ipynb`; all other trained models (majority baseline, logistic regression) are included under `results/models/`.
5. `random_state=42` is fixed throughout, so reruns reproduce the committed `results/` exactly.
