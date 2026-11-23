# Market Analysis and Stock Segmentation Using RFM

**Module:** 6BUIS017C CRM & CM With Business Intelligence, Individual Coursework CWK1 (CRM Case Study)
**Student:** Abarni Thiruthaniesan | UOW ID: 20519610 | IIT ID: 20231054

This repository contains the Google Colab notebook, data snapshot and outputs for my CWK1 analysis. The analysis segments S&P 500 shares using risk and return features (mean weekly return, beta) and RFM-style trading-activity features (Recency, Frequency, Monetary).

## Repository contents

| File | Description |
|---|---|
| `Abarni_CWK1_SP500_RFM.ipynb` | Complete notebook (Tasks 1 to 3), saved with all outputs |
| `cwk1_data.zip` | Data snapshot used in the final run; also the notebook's cached fallback dataset |
| `cwk1_all_outputs.zip` | All outputs: feature tables, logs, cluster results, data mart tables and figures |
| `requirements.txt` | Package versions used in the final run |

## Key outputs (inside `cwk1_all_outputs.zip`)

| Requirement | File |
|---|---|
| Feature table (one row per included share) with cluster assignments for the four baseline solutions | `outputs/feature_table_with_clusters.csv` |
| Share selection and exclusions | `outputs/inclusion_log.csv`, `outputs/exclusion_log.csv` |
| RFM correlation table | `outputs/rfm_correlation.csv` |
| Data mart tables (Task 3.1) | `outputs/data_mart/` |
| Figures (dendrograms, profiles, cluster plots) | `outputs/figures/` |
| Observation date, settings and package versions | `outputs/run_metadata.json` |

## Study design

- **Constituents:** current S&P 500 list from Wikipedia (503 tickers listed)
- **Prices and volume:** Yahoo Finance via `yfinance`, `auto_adjust=False` (Close, Adj Close and Volume)
- **Benchmark:** ^GSPC (S&P 500 index)
- **Study period:** 2021-01-01 to 2025-01-01 (end date exclusive); observation date 2024-12-31
- **Data retrieved:** 2026-11-23
- **Shares retained:** 486 (17 excluded by the Task 1.2 validation rules; see `exclusion_log.csv`)
- **Clustering:** Ward and K-means (random seed 42, `n_init=50`) on two separately standardised matrices: return and beta, and R, F, log1p(M); k = 3 selected for all four solutions

## How to run

1. Open `Abarni_CWK1_SP500_RFM.ipynb` in Google Colab.
2. Select **Runtime > Run all**.
3. The notebook downloads live data first. The acquisition cell prints the data source used and the retrieval date.

## Cached-data fallback

If live access to Wikipedia or Yahoo Finance fails or returns an incomplete download, the notebook automatically loads the cached snapshot. It uses the local `data/` folder if present; otherwise it downloads `cwk1_data.zip` from this repository. The snapshot covers the same study period. Its `snapshot_metadata.json` records the original retrieval date, sources, `yfinance` version and settings, so a cached run reports the true retrieval date alongside the notebook run date.

To test the fallback, set `FORCE_CACHE = True` in the settings cell, run all, then set it back to `False`.

## Reproducibility

Run settings and package versions are saved in `outputs/run_metadata.json`. Live data from Yahoo Finance can be revised over time, so the cached snapshot gives the exact data behind the reported results.
