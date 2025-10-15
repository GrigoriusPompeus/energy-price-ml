# NEM 5‑Minute Spot‑Price Nowcast Analysis

*A very short guide — read the notebook for details:* `NEM_Price_Nowcast_Analysis.ipynb`

## What it is
A compact, reproducible **nowcasting** workflow for Australia's National Electricity Market (NEM) 5‑minute spot prices (**RRP**).

## Project Structure
```
NEM 5-Minute Spot-Price Nowcast Analysis/
├── README.md
├── requirements.txt
├── .gitignore
├── NEM_Price_Nowcast_Analysis.ipynb    # Main analysis
├── data/
│   └── raw/                             # AEMO CSV files (not tracked)
└── exports/                             # Results (not tracked)
```

## Data
- **Source:** AEMO public data (dispatch/price & demand feeds).
- **Regions:** QLD1, NSW1, VIC1 (Queensland, New South Wales, Victoria).
- **Target:** RRP (regional reference price).
- **Frequency:** 5-minute settlement intervals.
- **Files needed:** Download from [AEMO Data Portal](https://nemweb.com.au/Reports/Current/MMSDataModelReport/)
  - Navigate to: Reports → Archive → Price and Demand
  - Pattern: `PRICE_AND_DEMAND_YYYYMM_REGION.csv`
  - Place in `data/raw/` directory

## Features
- **Outlier Detection:** Identifies and removes extreme price anomalies (e.g., $20,000+ spikes)
- **Feature Engineering:** Lag features (1-6 periods) + calendar features (hour, day of week)
- **Temporal Validation:** Time-based train/test split (last 7 days as test set)
- **Interactive Visualisations:** Plotly-based charts for exploration

## Methods (brief)
- **Models:** LinearRegression (baseline), RandomForest, XGBoost
- **Evaluation:** MAE, RMSE, R² (MAE is primary metric)
- **Approach:** Train separate models per region, export predictions to CSV

## Run
```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab  # open the notebook above
```

## Notebook Map
1. **Imports** - Load libraries
2. **Data Loading** - Read CSV files from data/raw/
3. **Data Cleaning** - Handle missing values, data types
4. **Outlier Detection** - Remove extreme price spikes
5. **EDA** - Visualise price and demand patterns
6. **Feature Engineering** - Create lag and calendar features
7. **Train/Test Split** - Temporal split (last 7 days = test)
8. **Model Training** - Train 3 models per region
9. **Performance Summary** - Compare metrics across regions
10. **Visualisations** - Interactive Plotly charts
11. **Export Results** - Save to exports/ directory

## Results
Model predictions and metrics are saved to `exports/`:
- `actual_vs_pred_<REGION>.csv` - Actual vs predicted prices
- `metrics_<REGION>.json` - Performance metrics (MAE, RMSE, R²)

> Tip: Execute top‑to‑bottom; each section is short and self‑contained.

## Licence
Data sourced from AEMO. See [AEMO's copyright notice](https://www.aemo.com.au/privacy-and-legal-notices/copyright-permissions) for terms.
