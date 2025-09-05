# Code & Data for "Day-Ahead Load Forecasting with GRU, XGBoost, and Hybrid Models"

This repository contains **four** Jupyter notebooks that all read from **`ost_data1.csv`** and save figures (600 dpi) in the **same folder** as the notebook files.

## Notebooks (place them in `code/`)
- `GRU.ipynb` — GRU model
- `XGB.ipynb` — XGBoost model
- `GRUXGB.ipynb` — Hybrid GRU+XGBoost (full)
- `Hibrid.ipynb` — Hybrid without holiday features *(rename if your mapping differs)*

> All four notebooks expect the dataset file **`ost_data1.csv`** in the **same folder** (`code/`).

## Quick start
```bash
# Option A: pip
pip install -r requirements.txt

# Open Jupyter and run the notebooks in order
# (Optional order) GRU -> XGB -> GRUXGB -> Hibrid
```

### Reproducibility header (put as the **first cell** in each notebook)
Copy the contents of [`code/REPRO_HEADER.py`](code/REPRO_HEADER.py) into a new code cell at the top of every notebook.  
Use `savefig("figure_name")` to export 600-dpi PNGs in the same folder.

## Data
- Expected path: `code/ost_data1.csv` (CSV size example: ~721 KB)
- If you cannot include the CSV in the repo (e.g., licensing), add a download link here and ensure the file is placed next to the notebooks.

## Results
- Figures are saved in `code/` as `.png` with `dpi=600`.

## Citation
If you use this code, please cite this repository. A `CITATION.cff` file is provided for GitHub's citation panel.
If you archive on Zenodo, add the DOI here and to `CITATION.cff`:

> DOI: 10.5281/zenodo.XXXXXXX

## License
Released under the MIT License — see `LICENSE`.
