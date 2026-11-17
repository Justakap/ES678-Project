# Paper Results Summary

Consolidated from existing saved artifacts only. No model was retrained, no metric was recalculated, and no experiment artifact was modified to produce this document. Source files are cited under each section. **Validation and test results are reported in clearly separated sections — do not compare numbers across them as if they were the same evaluation.**

---

## 1. Validation Results — All Models, Splits, Feature Conditions

Source: `results/model_comparison.csv` (no-`duration`), `results/leakage_comparison.csv` (with-`duration`). Validation n = 6,178 for every row.

| Split | Model | Feature set | Prevalence | AP | ROC-AUC | F1 | Precision | Recall | Accuracy |
|---|---|---|---|---|---|---|---|---|---|
| Stratified | Majority baseline | no_duration | 0.1127 | 0.1127 | 0.500 | 0 | 0 | 0 | 0.8873 |
| Stratified | Logistic Regression | no_duration | 0.1127 | 0.3989 | 0.7540 | 0.2674 | 0.7012 | 0.1652 | 0.8980 |
| Stratified | Random Forest | no_duration | 0.1127 | 0.3361 | 0.7368 | 0.3277 | 0.4656 | 0.2529 | 0.8831 |
| Stratified | Logistic Regression | with_duration | 0.1127 | 0.5732 | 0.9151 | 0.4728 | 0.6811 | 0.3621 | — (not in leakage_comparison.csv) |
| Stratified | Random Forest | with_duration | 0.1127 | 0.6055 | 0.9186 | 0.4843 | 0.6788 | 0.3764 | — (not in leakage_comparison.csv) |
| Chronological | Majority baseline | no_duration | 0.1065 | 0.1065 | 0.500 | 0 | 0 | 0 | 0.8935 |
| Chronological | Logistic Regression | no_duration | 0.1065 | 0.1978 | 0.6573 | 0 | 0 | 0 | 0.8935 |
| Chronological | Random Forest | no_duration | 0.1065 | 0.1873 | 0.6119 | 0.0780 | 0.4667 | 0.0426 | 0.8928 |
| Chronological | Logistic Regression | with_duration | 0.1065 | 0.4293 | 0.8771 | 0.2376 | 0.5868 | 0.1489 | — (not in leakage_comparison.csv) |
| Chronological | Random Forest | with_duration | 0.1065 | 0.4874 | 0.8819 | 0.2059 | 0.6723 | 0.1216 | — (not in leakage_comparison.csv) |

**⚠ Flagged gap**: `leakage_comparison.csv` does not include an `accuracy` column for the with-`duration` rows (unlike `model_comparison.csv`, which has it for no-`duration` rows). This value is not available from saved artifacts and is left blank rather than estimated.

---

## 2. Final Test Results — All Models, Splits, Feature Conditions

Source: `results/final/test_metrics.csv`. Test n = 6,179 for every row. Metrics shown at the **frozen validation-selected threshold** (see Section 5 for the thresholds themselves and the 0.5-threshold comparison).

| Split | Model | Feature set | Model category | Prevalence | AP | ROC-AUC | Precision | Recall | F1 |
|---|---|---|---|---|---|---|---|---|---|
| Stratified | Majority baseline | no_duration | realistic_pre_contact_model | 0.1126 | 0.1126 | 0.500 | 0 | 0 | 0 |
| Stratified | Logistic Regression | no_duration | realistic_pre_contact_model | 0.1126 | 0.4351 | 0.7831 | 0.4047 | 0.5460 | 0.4648 |
| Stratified | Random Forest | no_duration | realistic_pre_contact_model | 0.1126 | 0.3499 | 0.7396 | 0.3170 | 0.5201 | 0.3939 |
| Stratified | Logistic Regression | with_duration | **LEAKAGE_DIAGNOSTIC_ONLY_NOT_DEPLOYABLE** | 0.1126 | 0.5627 | 0.9192 | 0.5172 | 0.6925 | 0.5921 |
| Stratified | Random Forest | with_duration | **LEAKAGE_DIAGNOSTIC_ONLY_NOT_DEPLOYABLE** | 0.1126 | 0.5861 | 0.9136 | 0.5133 | 0.7227 | 0.6002 |
| Chronological | Majority baseline | no_duration | realistic_pre_contact_model | 0.3845 | 0.3845 | 0.500 | 0 | 0 | 0 |
| Chronological | Logistic Regression | no_duration | realistic_pre_contact_model | 0.3845 | 0.4682 | 0.6053 | 0.4928 | 0.3598 | 0.4160 |
| Chronological | Random Forest | no_duration | realistic_pre_contact_model | 0.3845 | 0.4621 | 0.6053 | 0.4835 | 0.4941 | 0.4888 |
| Chronological | Logistic Regression | with_duration | **LEAKAGE_DIAGNOSTIC_ONLY_NOT_DEPLOYABLE** | 0.3845 | 0.5463 | 0.7021 | 0.5580 | 0.5038 | 0.5295 |
| Chronological | Random Forest | with_duration | **LEAKAGE_DIAGNOSTIC_ONLY_NOT_DEPLOYABLE** | 0.3845 | 0.5304 | 0.6864 | 0.5449 | 0.5257 | 0.5351 |

Per `results/final/README.md`: with-`duration` models are explicitly labeled leakage diagnostics and are never to be treated as deployable, since `duration` is only known after a call ends.

---

## 3. AP and ROC-AUC Change from Adding `duration`

### Validation (source: `results/leakage_comparison.csv`)

| Split | Model | ΔAP | ΔROC-AUC |
|---|---|---|---|
| Stratified | Logistic Regression | +0.1743 | +0.1611 |
| Stratified | Random Forest | +0.2693 | +0.1818 |
| Chronological | Logistic Regression | +0.2315 | +0.2198 |
| Chronological | Random Forest | +0.3000 | +0.2700 |

### Test (source: `results/final/leakage_test_delta.csv`)

| Split | Model | ΔAP | ΔROC-AUC |
|---|---|---|---|
| Stratified | Logistic Regression | +0.1276 | +0.1360 |
| Stratified | Random Forest | +0.2363 | +0.1740 |
| Chronological | Logistic Regression | +0.0781 | +0.0968 |
| Chronological | Random Forest | +0.0684 | +0.0811 |

**⚠ Flagged inconsistency**: the leakage effect shrinks substantially from validation to test, and far more so for the chronological split than the stratified split:
- Stratified: RF ΔAP 0.2693 (val) → 0.2363 (test), a ~12% relative drop.
- Chronological: RF ΔAP 0.3000 (val) → 0.0684 (test), a **~77% relative drop**; LR 0.2315 → 0.0781, a ~66% drop.

This is consistent with the large prevalence shift noted in Section 7, but it means the validation-set leakage magnitude is not a reliable estimate of the test-set leakage magnitude for the chronological split specifically.

---

## 4. Bootstrap Confidence Intervals (Validation Only)

Source: `results/depth/bootstrap_ap_difference.csv`. Paired bootstrap, 1,000 resamples, n = 6,178 per split. **This analysis exists only for validation data** — no equivalent bootstrap CI was computed on the test set in any saved artifact.

| Split | Model | Observed ΔAP | 95% CI |
|---|---|---|---|
| Stratified | Logistic Regression | +0.1743 | [+0.1336, +0.2101] |
| Stratified | Random Forest | +0.2693 | [+0.2364, +0.2987] |
| Chronological | Logistic Regression | +0.2315 | [+0.1962, +0.2691] |
| Chronological | Random Forest | +0.3000 | [+0.2653, +0.3410] |

All four intervals exclude zero, i.e. the leakage-driven AP increase is statistically distinguishable from zero on validation data for every split/model combination.

**⚠ Flagged gap**: no bootstrap CI exists for the test-set ΔAP values in Section 3 — those test deltas are point estimates only, with no uncertainty quantification available from saved artifacts.

---

## 5. Validation-Selected Thresholds and Corresponding Test Metrics

Source: `results/final/test_metrics.csv` (`frozen_threshold` column, originally selected in `results/frozen_evaluation_config.json` from validation data only — threshold grid 0.05–0.95, step 0.05, maximizing F1).

| Split | Model | Feature set | Frozen threshold | Test Precision | Test Recall | Test F1 | *(for comparison)* F1 @ 0.5 |
|---|---|---|---|---|---|---|---|
| Stratified | Logistic Regression | no_duration | 0.15 | 0.4047 | 0.5460 | 0.4648 | 0.2919 |
| Stratified | Random Forest | no_duration | 0.20 | 0.3170 | 0.5201 | 0.3939 | 0.3210 |
| Stratified | Logistic Regression | with_duration | 0.20 | 0.5172 | 0.6925 | 0.5921 | 0.4804 |
| Stratified | Random Forest | with_duration | 0.30 | 0.5133 | 0.7227 | 0.6002 | 0.4974 |
| Chronological | Logistic Regression | no_duration | 0.10 | 0.4928 | 0.3598 | 0.4160 | 0.1815 |
| Chronological | Random Forest | no_duration | 0.15 | 0.4835 | 0.4941 | 0.4888 | 0.0805 |
| Chronological | Logistic Regression | with_duration | 0.05 | 0.5580 | 0.5038 | 0.5295 | 0.2581 |
| Chronological | Random Forest | with_duration | 0.15 | 0.5449 | 0.5257 | 0.5351 | 0.1689 |
| Stratified / Chronological | Majority baseline | no_duration | N/A (no tuned threshold; constant probability output) | 0 | 0 | 0 | 0 |

Every frozen threshold improved test F1 over the default 0.5 threshold, in some cases dramatically (chronological RF no_duration: 0.0805 → 0.4888).

**⚠ Flagged gap**: `results/depth/threshold_sensitivity.csv` (the validation threshold-sweep table) only contains sweep data for the two no-`duration` models; it has no rows for `with_duration` models or the `majority_baseline`. The with-`duration` frozen thresholds reported above and in `test_metrics.csv` trace back to `frozen_evaluation_config.json`, which independently computed that sweep — this is consistent across files, but the intermediate with-`duration` sweep table itself does not exist as a separate saved artifact.

---

## 6. Confusion Matrices

### Validation (source: `results/model_comparison.csv`, no-`duration` only; with-`duration` confusion matrices are not present in `leakage_comparison.csv`)

| Split | Model | TN | FP | FN | TP |
|---|---|---|---|---|---|
| Stratified | Majority baseline | 5482 | 0 | 696 | 0 |
| Stratified | Logistic Regression | 5433 | 49 | 581 | 115 |
| Stratified | Random Forest | 5280 | 202 | 520 | 176 |
| Chronological | Majority baseline | 5520 | 0 | 658 | 0 |
| Chronological | Logistic Regression | 5520 | 0 | 658 | 0 |
| Chronological | Random Forest | 5488 | 32 | 630 | 28 |

**⚠ Flagged gap**: no confusion matrix for with-`duration` models exists on validation data in any saved CSV (`leakage_comparison.csv` has precision/recall/F1 but not TN/FP/FN/TP counts).

### Test, at threshold 0.5 (source: `results/final/test_metrics.csv`)

| Split | Model | Feature set | TN | FP | FN | TP |
|---|---|---|---|---|---|---|
| Stratified | Majority baseline | no_duration | 5483 | 0 | 696 | 0 |
| Stratified | Logistic Regression | no_duration | 5424 | 59 | 567 | 129 |
| Stratified | Random Forest | no_duration | 5274 | 209 | 523 | 173 |
| Stratified | Logistic Regression | with_duration | 5363 | 120 | 438 | 258 |
| Stratified | Random Forest | with_duration | 5315 | 168 | 410 | 286 |
| Chronological | Majority baseline | no_duration | 3803 | 0 | 2376 | 0 |
| Chronological | Logistic Regression | no_duration | 3474 | 329 | 2106 | 270 |
| Chronological | Random Forest | no_duration | 3699 | 104 | 2272 | 104 |
| Chronological | Logistic Regression | with_duration | 3533 | 270 | 1984 | 392 |
| Chronological | Random Forest | with_duration | 3632 | 171 | 2141 | 235 |

### Test, at frozen threshold (source: `results/final/test_metrics.csv`)

| Split | Model | Feature set | TN | FP | FN | TP |
|---|---|---|---|---|---|---|
| Stratified | Logistic Regression | no_duration | 4924 | 559 | 316 | 380 |
| Stratified | Random Forest | no_duration | 4703 | 780 | 334 | 362 |
| Stratified | Logistic Regression | with_duration | 5033 | 450 | 214 | 482 |
| Stratified | Random Forest | with_duration | 5006 | 477 | 193 | 503 |
| Chronological | Logistic Regression | no_duration | 2923 | 880 | 1521 | 855 |
| Chronological | Random Forest | no_duration | 2549 | 1254 | 1202 | 1174 |
| Chronological | Logistic Regression | with_duration | 2855 | 948 | 1179 | 1197 |
| Chronological | Random Forest | with_duration | 2760 | 1043 | 1127 | 1249 |

(Majority baseline at frozen threshold is identical to its 0.5-threshold row, since it has no tuned threshold.)

---

## 7. Temporal Distribution Findings

Source: `results/eda/segment_subscription_rates.csv`, `results/eda/segment_rate_changes_ranked.csv`, `results/eda/month_distribution_by_chronological_split.csv`.

**10 equal row-index segments (earliest → latest), subscription rate**:

| Segment | Rows | Subscription rate |
|---|---|---|
| 1 | 0–4117 | 2.77% |
| 2 | 4118–8236 | 3.52% |
| 3 | 8237–12355 | 4.22% |
| 4 | 12356–16474 | 6.63% |
| 5 | 16475–20593 | 6.24% |
| 6 | 20594–24711 | 5.46% |
| 7 | 24712–28830 | 10.15% |
| 8 | 28831–32949 | 11.99% |
| 9 | 32950–37068 | 15.73% |
| 10 | 37069–41187 | **45.93%** |

**Largest segment-to-segment jump**: segment 9 → 10, **+30.20 percentage points** (15.73% → 45.93%) — by far the largest change in the series (next largest is +4.68pp, segment 6→7).

**Chronological split / month cross-tabulation**: several months fall almost entirely into a single split — `jun`, `jul`, `aug`, `oct`, `dec` are 94–100% train-only; `sep` is 100% test-only (570/570 rows); `apr` splits across train/val/test unevenly (859/1599/174).

**⚠ Directly explains the validation/test prevalence mismatch** reported in the companion test-evaluation notebook: chronological validation prevalence is 10.65% while chronological test prevalence is 38.45% — this is a direct consequence of segment 10 (45.93% prevalence) falling inside the test portion of the chronological split.

---

## 8. Failure-Mode Findings (Validation Set, Realistic/No-Duration Models Only)

Source: `results/depth/failure_mode_overall.csv`, `results/depth/failure_mode_by_job.csv`, `results/depth/failure_mode_by_poutcome.csv`. Subgroups with fewer than 100 validation rows are excluded by design (not computed, not a gap).

### Overall (n = 6,178 per split)

| Split | Model | FN rate | FP rate |
|---|---|---|---|
| Stratified | Logistic Regression | 83.48% | 0.89% |
| Stratified | Random Forest | 74.71% | 3.68% |
| Chronological | Logistic Regression | 100.00% | 0.00% |
| Chronological | Random Forest | 95.74% | 0.58% |

Chronological Logistic Regression has **zero true positives** (100% FN rate, 0 FP) at the default threshold — it predicts "no" for every validation row.

### By `job` (subgroups ≥ 100 rows)

- **Stratified LR**: highest FP rate in `retired` (9.60%, n=237) and `student` (7.32%, n=132); lowest FN rate also in `retired` (56.67%) and `unemployed` (72.22%).
- **Stratified RF**: highest FP rate in `student` (12.20%, n=132) and `retired` (11.30%, n=237).
- **Chronological LR**: FN rate is exactly 100% and FP rate exactly 0% in **every** job subgroup (9 subgroups meet the size threshold; `unemployed` and `housemaid` are excluded as <100 rows) — consistent with the model predicting no positives at all.
- **Chronological RF**: `retired` again stands out with the highest FP rate (12.63%, n=128) and lowest FN rate (69.70%) among chronological subgroups.

### By `poutcome` (subgroups ≥ 100 rows; 3 categories meet the threshold in both splits: `nonexistent`, `failure`, `success`)

- **Stratified LR**: `success` subgroup (previously subscribed) has by far the highest FP rate (49.23%, n=187, only 65 actual negatives) and lowest FN rate (13.93%) — the model over-predicts "yes" here.
- **Stratified RF**: same pattern, even more pronounced (`success` FP rate 60.00%).
- **Chronological LR**: FP rate 0% and FN rate 100% in all three `poutcome` subgroups (same no-positive-predictions behavior as above).
- **Chronological RF**: `success` subgroup FN rate is 100% (67/67 actual positives missed) despite only 1 false positive — essentially blind to this subgroup, in contrast to the stratified split where the same subgroup is the model's best-performing one.

**⚠ Flagged inconsistency**: the `poutcome = success` subgroup behaves in opposite directions across the two splits — strongly over-predicted "yes" (high recall, high FP rate) under the stratified split, but almost entirely missed (FN rate 100% for chronological RF) under the chronological split. This is a direct downstream consequence of the same train/test distributional differences noted in Sections 3 and 7, not a contradiction in the saved data itself.

---

## Index of Source Files Used

- `results/model_comparison.csv`
- `results/leakage_comparison.csv`
- `results/depth/bootstrap_ap_difference.csv`
- `results/depth/threshold_sensitivity.csv`
- `results/depth/failure_mode_overall.csv`
- `results/depth/failure_mode_by_job.csv`
- `results/depth/failure_mode_by_poutcome.csv`
- `results/eda/segment_subscription_rates.csv`
- `results/eda/segment_rate_changes_ranked.csv`
- `results/eda/month_distribution_by_chronological_split.csv`
- `results/final/test_metrics.csv`
- `results/final/leakage_test_delta.csv`
- `results/final/README.md`
- `results/frozen_evaluation_config.json` (referenced indirectly via `test_metrics.csv`'s `frozen_threshold` column)

No dataset file, split-index file, or fitted model file was read, modified, or recomputed to produce this summary.
