# Final Test Evaluation — Model Labeling

- `model_category == "realistic_pre_contact_model"`: the no-`duration` models (`majority_baseline`, `logistic_regression`, `random_forest`). These use only features known before a scheduled contact and are the only ones that could realistically be deployed.

- `model_category == "LEAKAGE_DIAGNOSTIC_ONLY_NOT_DEPLOYABLE"`: the with-`duration` `logistic_regression` / `random_forest` models. `duration` is only known after a call ends, so these models' apparently strong performance is a measurement of leakage, not a usable pre-contact predictor. **Do not deploy these.**
