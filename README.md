# Bitcoin Price Prediction on BTCUSDT 15-Minute Data

A complete time-series-oriented machine learning project investigating whether robust prediction signals can be derived from historical BTCUSDT spot-market data and remain economically useful after transaction costs.

The project covers the full pipeline from data acquisition, data quality, exploratory analysis, feature and target engineering, walk-forward validation, baseline models, hyperparameter tuning, and probability calibration to cost-aware threshold selection and final strategy feasibility analysis.

> **Final result:**  
> For the investigated data, features, models, prediction horizons, and cost assumptions, no candidate passed the predefined Economic Gate under realistic round-trip costs. Therefore, no model was approved for the final test split or for live trading.

---

## 1. Research Question

The central research question is:

> Can statistically reliable directional signals be generated from BTCUSDT 15-minute market data that remain economically robust after fees, spread, and slippage?

Three prediction horizons were investigated:

| Horizon | Candles | Time span |
|---|---:|---:|
| h4 | 4 | 1 hour |
| h16 | 16 | 4 hours |
| h96 | 96 | 24 hours |

The focus is not limited to classification metrics. A model is considered relevant only if it also passes a predefined economic robustness gate.

---

## 2. Key Results

| Horizon | Final model considered | Calibration | Threshold decision | Maximum robust cost | Current costs feasible |
|---|---|---|---|---:|---|
| h4 | LightGBM | Sigmoid | `no_trade` | 5 bp | No |
| h16 | CatBoost | Sigmoid | `no_trade` | 10 bp | No |
| h96 | LightGBM | Raw | `no_trade` | 5 bp | No |

Current round-trip cost assumption:

```text
31.9744 basis points
```

h16 showed the strongest exploratory cost robustness. However, it still remained well below the assumed realistic cost level.

### Technical Interpretation

The result does not mean that Bitcoin is fundamentally unpredictable.

It means:

> With the data basis, feature set, model classes, validation methodology, and cost assumptions used in this project, no sufficiently robust and economically viable trading signal could be demonstrated.

The conservative `No Trade` decision is therefore a valid and methodologically correct project outcome.

---

## 3. Methodological Principles

The project follows several binding rules.

### Time-Series-Aware Validation

- no random mixing of future and past data;
- walk-forward or expanding-window folds;
- temporal separation of training, validation, holdout, and final test;
- horizon-dependent purging and embargo logic;
- fold-based model and calibration selection.

### Leakage Protection

- no target columns in the feature set;
- no use of future timestamps;
- no selection based on the final test set;
- holdout used only once to confirm decisions already based on cross-validation;
- threshold selection exclusively on inner training segments;
- Economic Gate evaluated on outer walk-forward folds.

### Economic Evaluation

The models were not evaluated solely by Accuracy, ROC-AUC, or Log Loss.

The evaluation also considered:

- transaction fees;
- bid-ask spread;
- slippage;
- round-trip costs;
- minimum number of trades;
- proportion of tradable folds;
- positive outer-fold returns;
- profit factor;
- net-return lower confidence bound;
- stability across multiple cost levels;
- `No Trade` as a genuine comparison alternative.

---

## 4. Project Status

| Area | Status |
|---|---|
| Data pipeline | Completed |
| Data quality | Completed |
| Exploratory data analysis | Completed |
| Feature engineering | Completed |
| Target engineering | Completed |
| Dataset building | Completed |
| Walk-forward splitting | Completed |
| Baseline models | Completed |
| Model training | Completed |
| Hyperparameter tuning | Completed |
| Calibration | Completed |
| Threshold selection | Completed |
| Economic Gate | Completed |
| Strategy feasibility | Completed |
| Final test | Not opened |
| Production approval | Not granted |
| Project decision | `No Trade` |

---

## 5. Project Structure

```text
BTC TSP 15min/
├── config.py
├── data_pipeline.py
├── data_quality.py
├── eda.py
├── feature_engineering.py
├── target_engineering.py
├── dataset_builder.py
├── time_series_splitter.py
├── baseline_models.py
├── model_training.py
├── hyperparameter_tuning.py
├── calibration_evaluation.py
├── threshold_signal_optimization.py
├── strategy_feasibility_analysis.py
├── h16_screening.py
├── h96_screening.py
├── final_project_report.py
│
├── data/
│   ├── raw/
│   ├── interim/
│   └── processed/
│       ├── candles/
│       ├── features/
│       ├── targets/
│       ├── datasets/
│       └── splits/
│
├── models/
│   └── artifacts/
│
├── reports/
│   ├── data_quality/
│   ├── eda/
│   ├── feature_engineering/
│   ├── target_engineering/
│   ├── model_training/
│   ├── hyperparameter_tuning/
│   ├── threshold_signal_optimization/
│   ├── strategy_feasibility_analysis/
│   ├── h16_screening/
│   ├── h96_screening/
│   └── final/
│       ├── input_validation.json
│       ├── source_runs.json
│       ├── horizon_comparison.csv
│       ├── model_comparison.csv
│       ├── cost_feasibility_comparison.csv
│       ├── cost_threshold_surface_combined.csv
│       ├── final_summary.json
│       ├── final_conclusion.md
│       ├── artifact_manifest.json
│       └── figures/
│
├── notebooks/
│   ├── 01_data_audit.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_target_engineering.ipynb
│   ├── 05_dataset_and_splitting.ipynb
│   ├── 06_model_training_evaluation.ipynb
│   ├── 07_baseline_models.ipynb
│   ├── 08_hyperparameter_tuning_and_calibration.ipynb
│   ├── 09_threshold_and_strategy_feasibility.ipynb
│   └── 10_final_project_results.ipynb
│
├── requirements-lock.txt
├── python-version.txt
└── README.md
```

The actual directory structure may differ slightly for older runs. In particular, h4 was created before horizon-specific screening directories were introduced.

---

## 6. Technical Environment

The final report was generated in the following environment:

```text
Python 3.14.5
Linux
virtual Python environment
```

Project root of the original execution:

```text
/home/milan/uni/python/BTC TSP/BTC TSP 15min
```

Virtual environment of the original execution:

```text
/home/milan/uni/python/BTC TSP/.venv
```

---

## 7. Installation

### 7.1 Open the Repository

```bash
cd "/home/milan/uni/python/BTC TSP/BTC TSP 15min"
```

### 7.2 Activate the Virtual Environment

```bash
source "../.venv/bin/activate"
```

Alternative:

```bash
source "/home/milan/uni/python/BTC TSP/.venv/bin/activate"
```

### 7.3 Install Dependencies

When a lock file is available:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements-lock.txt
```

When only a standard requirements file is available:

```bash
python -m pip install -r requirements.txt
```

### 7.4 Verify the Installation

```bash
python --version
python -m pip check
```

---

## 8. Dataset

The data pipeline creates a canonical BTCUSDT 15-minute candle dataset from:

- historical Binance archives;
- API-based updates;
- consolidated OHLCV and trade data;
- UTC-normalized timestamps.

The datasets are generated locally and are not necessarily fully versioned with the repository because of their size.

Typical canonical candle path:

```text
data/processed/candles/BTCUSDT_15m_candles.parquet
```

### Data Quality Checks

The following aspects are checked, among others:

- schema and data types;
- missing values;
- duplicates;
- timestamp ordering;
- candle interval;
- OHLC logic;
- negative values;
- zero volume;
- number of trades;
- temporal gaps;
- unusual outliers;
- open-time and close-time consistency.

---

## 9. Execution Order

The modules generally use a CLI pattern with the `run` command.

The exact options of a module can be displayed with:

```bash
python <module>.py --help
```

### 9.1 Data Pipeline

```bash
python data_pipeline.py run
```

### 9.2 Data Quality

```bash
python data_quality.py run
```

### 9.3 Exploratory Data Analysis

```bash
python eda.py run
```

### 9.4 Feature Engineering

```bash
python feature_engineering.py run
```

### 9.5 Target Engineering

```bash
python target_engineering.py run
```

### 9.6 Dataset Building

```bash
python dataset_builder.py run
```

### 9.7 Time-Series Splitting

```bash
python time_series_splitter.py run
```

### 9.8 Baseline Models

```bash
python baseline_models.py run
```

### 9.9 Model Training

```bash
python model_training.py run
```

### 9.10 Hyperparameter Tuning

```bash
python hyperparameter_tuning.py run
```

### 9.11 Calibration

```bash
python calibration_evaluation.py run
```

### 9.12 Threshold Selection

```bash
python threshold_signal_optimization.py run
```

### 9.13 Strategy Feasibility

```bash
python strategy_feasibility_analysis.py run
```

For complete reproduction, use the exact parameters stored in the corresponding report JSON files and logs.

---

## 10. Frozen Final Runs

The final aggregation uses the following reference runs:

### h4

```text
reports/threshold_signal_optimization/20260729T202947619086Z
```

### h16

```text
reports/h16_screening/h16_20260730T022812
```

### h96

```text
reports/h96_screening/h96_20260730T075624
```

h4 originates from an older report structure. h16 and h96 were generated using the later screening orchestrators.

---

## 11. Generate the Final Project Report

```bash
python final_project_report.py run \
    --h4-run-dir \
    "reports/threshold_signal_optimization/20260729T202947619086Z" \
    --h16-run-dir \
    "reports/h16_screening/h16_20260730T022812" \
    --h96-run-dir \
    "reports/h96_screening/h96_20260730T075624"
```

Alternatively, the module can automatically search for the latest suitable runs:

```bash
python final_project_report.py run
```

### Validation

```bash
python final_project_report.py validate
```

### Status

```bash
python final_project_report.py status
```

### Expected Safety Conditions

```text
final_test_accessed = false
training_executed = false
tuning_executed = false
threshold_optimized = false
test_split_opened_by_this_program = false
```

`final_project_report.py` is a pure aggregation module. It does not execute training, tuning, backtesting, or threshold optimization.

---

## 12. Notebook Order

The notebooks should be read or executed in the following order:

### Notebook 01 – Data Audit

- raw-data structure;
- schema;
- temporal coverage;
- data-quality overview.

### Notebook 02 – EDA

- price and return distributions;
- volume;
- volatility;
- correlations;
- time-series properties.

### Notebook 03 – Feature Engineering

- technical indicators;
- time-based features;
- rolling statistics;
- feature distributions;
- leakage checks.

### Notebook 04 – Target Engineering

- binary target variables;
- continuous forward returns;
- horizon definitions;
- class distributions.

### Notebook 05 – Dataset and Splitting

- feature-target merge;
- walk-forward folds;
- holdout and test definitions;
- purging and embargo.

### Notebook 06 – Model Training and Evaluation

- training pipeline;
- fold metrics;
- model artifacts;
- initial validation.

### Notebook 07 – Baseline Models

- simple statistical and machine learning baselines;
- reference metrics;
- comparison with more complex models.

### Notebook 08 – Hyperparameter Tuning and Calibration

- Optuna results;
- LightGBM and CatBoost;
- cross-validation stability;
- holdout confirmation;
- raw and sigmoid calibration.

### Notebook 09 – Threshold and Strategy Feasibility

- threshold selection;
- Economic Gate;
- fold decisions;
- cost model;
- cost-threshold surfaces;
- `No Trade`.

### Notebook 10 – Final Project Results

- joint comparison of h4, h16, and h96;
- model and cost overview;
- final decision;
- artifact manifest;
- Definition of Done.

---

## 13. Authoritative Final Artifacts

The authoritative final source is:

```text
reports/final/
```

Important files:

### `final_summary.json`

Machine-readable overall summary.

### `final_conclusion.md`

Written technical conclusion.

### `horizon_comparison.csv`

Comparison of h4, h16, and h96.

### `model_comparison.csv`

Summary of model metrics and selections.

### `cost_feasibility_comparison.csv`

Comparison of cost robustness.

### `artifact_manifest.json`

Paths, file sizes, timestamps, and SHA-256 checksums of the used and generated artifacts.

### `input_validation.json`

Validation of final sources and safety conditions.

### `source_runs.json`

Frozen references to the final runs used.

---

## 14. Models

The project primarily investigated the following models:

- dummy and majority-class baselines;
- logistic or linear baselines;
- LightGBM;
- CatBoost.

Model selection was primarily based on time-series-aware cross-validation and Log Loss.

A better statistical metric alone did not lead to trading approval. Model and calibration selection was always followed by economic threshold and feasibility evaluation.

---

## 15. Calibration

At minimum, the following methods were compared:

- `raw`;
- `sigmoid`.

Selection was based on the walk-forward folds.

The holdout was not allowed to influence the selection of the calibration method.

Calibration may improve probability quality, but it does not create an economic signal when the underlying predictions are not robust after costs.

---

## 16. Threshold Selection

Threshold selection was performed in a nested manner within the walk-forward structure.

Core rules:

- thresholds are not optimized on the final test set;
- inner training segments determine the candidate;
- outer folds evaluate generalization;
- `No Trade` has an objective value of at least zero;
- a tradable candidate must robustly outperform `No Trade`;
- a diagnostic reference threshold is not executable when `decision=no_trade`.

---

## 17. Economic Gate

A candidate must satisfy several conditions simultaneously.

These may include:

- minimum share of tradable folds;
- minimum share of positive outer folds;
- minimum number of trades;
- positive mean net return;
- positive net-return lower confidence bound;
- positive total net return;
- profit factor greater than 1;
- sufficient stability;
- feasibility under realistic costs.

None of the investigated horizons passed the complete gate.

---

## 18. Final Test Split

The final test split remained closed.

This was a deliberate methodological decision:

1. Model development is performed exclusively on training data and walk-forward cross-validation.
2. The holdout is used at most once for confirmation.
3. Threshold and Economic Gate decisions are made before the final test.
4. Only a fully approved candidate may be evaluated once on the test set.
5. Since no candidate was approved, no final test evaluation was performed.

This prevents repeated decisions from indirectly turning the final test set into another validation set.

---

## 19. Reproducibility

### Store the Python Version

```bash
python --version > python-version.txt
```

### Freeze Package Versions

```bash
python -m pip freeze > requirements-lock.txt
```

### Check Syntax

```bash
python -m compileall .
```

### Verify Package Consistency

```bash
python -m pip check
```

### Validate the Final Report

```bash
python final_project_report.py validate
```

### Checksums

The final manifest stores SHA-256 checksums for relevant artifacts.

This allows verification that a report or source file has not been modified after project completion.

---

## 20. Known Limitations

### Older h4 Report Structure

h4 was created before the horizon-specific screening orchestrators were introduced. Its artifacts therefore reside in generic directories such as:

```text
reports/threshold_signal_optimization/
reports/strategy_feasibility_analysis/
```

Some detailed visualizations in Notebook 09 cannot automatically merge h4 with h16 and h96 in every cost-surface plot.

The authoritative h4 final values are still available in:

```text
reports/final/
10_final_project_results.ipynb
artifact_manifest.json
horizon_comparison.csv
cost_feasibility_comparison.csv
```

### Market Regimes

The results may depend on the market regimes contained in the dataset.

### Data Source

The project uses BTCUSDT spot-market data. The results are not automatically transferable to futures, other exchanges, or other trading pairs.

### Cost Model

Actual costs depend on factors including:

- exchange;
- fee tier;
- order type;
- liquidity;
- order size;
- spread;
- slippage;
- latency.

### Model Space

Only a limited model and feature space was investigated.

Examples of areas not investigated exhaustively include:

- order-book data;
- on-chain data;
- derivatives-market data;
- funding rates;
- liquidation data;
- news and sentiment data;
- cross-asset features;
- regime-switching models;
- neural sequence models;
- reinforcement learning;
- multi-asset portfolios.

### Statistical Significance

A positive observation in a single fold or cost level is not evidence of a robust strategy.

---

## 21. Future Work

Possible extensions of the project include:

1. more realistic maker and taker scenarios;
2. limit-order execution;
3. order-book and microstructure features;
4. dynamic volatility and regime detection;
5. adaptive horizons;
6. meta-labeling;
7. separate long and short models;
8. cross-exchange data;
9. probabilistic return distributions instead of binary targets only;
10. additional confirmatory runs with a fully prespecified protocol;
11. paper trading before any use of real capital.

These extensions should be treated as a new research phase. The completed results must not be reinterpreted or overwritten retrospectively.

---

## AI Usage Disclosure

OpenAI GPT-5.6 Thinking was used to support language editing, document structuring, code review, and visualization drafting. All methodology, implementation decisions, experiments, results, and conclusions were reviewed and validated by the author.

---

## 22. Out of Scope

This repository does not constitute investment advice and is not a production-ready trading system.

It does not provide:

- a guarantee of future returns;
- a recommendation to buy or sell Bitcoin;
- automated live-order execution;
- approval to use real capital;
- any claim that past performance predicts future performance.

---

## 23. Definition of Done

The project is considered technically complete when:

- [x] the data pipeline is reproducible;
- [x] data quality has been checked;
- [x] exploratory data analysis has been documented;
- [x] features and targets are generated transparently;
- [x] walk-forward splits are available;
- [x] baseline models have been evaluated;
- [x] LightGBM and CatBoost have been evaluated;
- [x] hyperparameter tuning has been documented;
- [x] probability calibration has been performed;
- [x] threshold selection was nested;
- [x] realistic costs were considered;
- [x] `No Trade` was included as an alternative;
- [x] h4, h16, and h96 were compared;
- [x] the final test was not used for selection decisions;
- [x] no unsuitable candidate was approved;
- [x] a final machine-readable report is available;
- [x] an artifact manifest with checksums is available;
- [x] a final results notebook is available;
- [x] limitations are documented.

---

## 24. Conclusion

The project demonstrates a complete and methodologically conservative machine learning pipeline for financial time series.

The investigated models showed some statistical signal and limited robust regions at low costs. However, these were insufficient to reliably overcome the assumed realistic round-trip cost burden.

The correct final decision is therefore:

```text
NO TRADE
```

No model was approved for the final test or for production use.
