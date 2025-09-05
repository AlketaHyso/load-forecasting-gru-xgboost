# Day-Ahead Load Forecasting with GRU, XGBoost, and Hybrid Models

This study compares the predictive abilities of **Gated Recurrent Unit (GRU)** neural networks, **Extreme Gradient Boosting (XGBoost)**, and a **combined GRU–XGBoost** approach for **24-hour ahead electrical load estimation**. The repository provides reproducible notebooks and the CSV dataset used to generate the results.

## Repository contents
- `code/GRU.ipynb` — GRU model
- `code/XGB.ipynb` — XGBoost model
- `code/Hibrid.ipynb` — Hybrid **with** holiday features
- `code/GRUXGB.ipynb` — Hybrid GRU+XGBoost (**without** holiday features)
- `code/ost_data1.csv` — Dataset used by all notebooks (~721 KB)

Figures produced during execution are saved in `code/` as `.png` at **dpi=600**.

## Quick start
- **Python**: 3.11 recommended
- **Install dependencies**
  ```bash
  pip install -r requirements.txt
