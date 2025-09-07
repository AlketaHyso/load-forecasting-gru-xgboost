Day-Ahead Load Forecasting with GRU, XGBoost, and Hybrid Models

This project compares Gated Recurrent Unit (GRU) neural networks, Extreme Gradient Boosting (XGBoost), and a residual-based GRU→XGBoost hybrid for 24-hour ahead electrical load forecasting. The repository provides reproducible notebooks; data are obtained by the user from the official source.

## Repository structure

```text
.
├─ code/
│  ├─ GRU.ipynb                 # GRU for 24→24 forecasting
│  ├─ XGB.ipynb                 # XGBoost baseline with engineered features
│  ├─ Hibrid.ipynb              # Residual-based Hybrid (with holiday features)
│  ├─ GRUXGB.ipynb              # Hybrid GRU+XGBoost (without holiday features)
│  ├─ Correct_Data.ipynb        # Pre-read fixes: header separators & trailing commas
│  ├─ Cleanning.ipynb           # Structural cleaning & continuity (see README)
│  └─ ost_data_clean.csv        # Produced by Cleanning.ipynb
├─ requirements.txt
└─ README.md

Methods at a glance
GRU: sequence model on hourly load, calendar features, Fourier seasonality, optional cross-border exchanges; time-based split.
XGBoost: tree model on the engineered tabular features.
Hybrid (residual-based):
Train GRU and generate forecasts
Compute residuals (actual − forecast)
Train XGBoost on residuals with the same horizon-aligned tabular features
Final forecast = GRU forecast + XGBoost residual correction
Metrics: MAE, RMSE, MAPE, R² on a held-out test set.

Quick start
Python: 3.11 recommended

Setup
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
# source .venv/bin/activate
pip install -r requirements.txt jupyterlab

Launch JupyterLab
# With the virtual environment active:
jupyter lab

Data
code/ost_data_clean.csv

Model notebooks

Run GRU.ipynb → GRU forecasts + residuals
Run XGB.ipynb → XGBoost baseline
Run Hibrid.ipynb (with holidays)
Run GRUXGB.ipynb (without) → hybrid results

Data Source
Source: https://opendata.ost.al/
OST (Operatori i Sistemit të Transmetimit, Albania) — official portal: https://ost.al/.
Time span & format: Hourly operational data, 23 Feb 2024 – 1 Jul 2025, downloaded as CSV.

Manual corrections (performed by us before any notebook runs)
To ensure data quality, we apply the following manual fixes to the raw file upfront:
Total Load (19 Dec 2024, 10:00) recorded an impossible value of 49,248,784 [MW/MWh]. It was replaced with 1,122 [MW/MWh], computed as the median of the adjacent 09:00 and 11:00 values.
Total Production — 11 Jul 2024 10:00: 32,408,672 MWh → 922 MWh (average of 09:00 & 11:00).
Output: code/ost_data_raw.csv.

Pre-read formatting (Correct_Data.ipynb)
Replace commas in the header with ;
Remove trailing commas at the end of each line
Read the CSV using sep=";" only
Output: code/ost_data.csv

Cleaning & continuity (Cleanning.ipynb)
This notebook performs structural cleaning and the targeted negative-load fix:
Parse Data + Ora to hourly timestamps; sort chronologically
Enforce numeric dtypes; standardize the column names used downstream
Drop duplicate timestamps/rows; validate basic ranges (flags only)
Ensure continuous hourly frequency; insert any missing hours
Negative “Total Load” — morning of 18 Sep 2024: replace using the median from a centered ±14-day window (29 points), then apply short linear interpolation to keep the series continuous
Output: code/ost_data_clean.csv (used by all modeling notebooks)

Pipeline outputs:
code/ost_data.csv — delimiter/row formatting normalized
code/ost_data_clean.csv — cleaned, continuous hourly series

Feature engineering (used in models)
Calendar: hour, day of week, weekend flag, month
Holidays (hybrid variant): AL/ME/XK/GR calendars
Seasonality: Fourier terms (daily/weekly)
Operations: cross-border physical exchanges and related OST fields
Scaling: fit on train only; time-ordered train/val/test (e.g., 70/10/20)

Reproducibility
Time-based splits to avoid leakage
Fixed random seeds where applicable (GRU/XGBoost)
Plots saved deterministically at 600 dpi directly under code/

License & attribution

Code: MIT License (see LICENSE).

How to cite
Day-Ahead Load Forecasting with GRU, XGBoost, and Hybrid Models (MIT License).
