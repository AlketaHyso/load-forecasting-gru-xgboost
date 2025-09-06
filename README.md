# Day-Ahead Load Forecasting with GRU, XGBoost, and Hybrid Models

We compare the predictive abilities of **Gated Recurrent Unit (GRU)** neural networks, **Extreme Gradient Boosting (XGBoost)**, and a **combined GRU–XGBoost** approach for **24-hour ahead electrical load estimation**. The repository provides reproducible notebooks and the CSV dataset used to generate the results.

## Repository contents
- `code/GRU.ipynb` — GRU model
- `code/XGB.ipynb` — XGBoost model
- `code/Hibrid.ipynb` — Hybrid **with** holiday features
- `code/GRUXGB.ipynb` — Hybrid GRU+XGBoost (**without** holiday features)
- `code/ost_data_clean.csv` — Dataset used by all notebooks (~721 KB)

Figures produced during execution are saved in `code/` as `.png` at **dpi=600**.

## Quick start
- **Python**: 3.11 recommended
- **Install dependencies**
  ```bash
  pip install -r requirements.txt
## Data
Source: OST (Operatori i Sistemit të Transmetimit, Albania) — https://ost.al/  
Terms: © 2025 OST. All rights reserved.
We do **not** redistribute OST data in this repository.  
Please download the dataset from the official portal and place it next to the notebooks as:
`code/ost_data_raw.csv`

We use publicly available hourly data from the Albanian Transmission System Operator (OST) obtained from the Open Data portal, which spans from 23 February 2024 to 1 July 2025. The dataset was downloaded in .csv format. A single erroneous value of 49,248,784 MWh appeared on 19 December 2024 at 10:00, and was replaced with 1,122 MWh—the median of the same-day 09:00 and 11:00 load values(Change it).Similarly, the “Prodhimi Total” (Total Production) entry for 11 July 2024 at 10:00 rec-orded 32,408,672 MWh; we replaced this impossible value with 922 MWh, computed as the average of the same day’s 09:00 and 11:00 readings (Change it).
Save the file as code/ost_data_raw.csv.
Execute file Correct_Data to clean the rows before reading; Replace the commas in the header with “;” and remove trailing commas from each line, then read using sep=";" only. We have now the file code/ost_data.csv.  
All instances of “Total Load” during morning hours of 18 September 2024, with negative values received replacement by using the median values from a ±14-day centered window that contained 29 data points. Linear interpolation was applied to smooth the corrected series for maintaining continuous time. These steps were implemented by executing file Cleanning.ipynb; the final file is code/ost_data_clean.csv
