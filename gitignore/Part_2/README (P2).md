# West Coast Housing Price Analysis & Predictor

**Tools:** Python · Pandas · Scikit-learn · Matplotlib · Seaborn · Parquet  
**Source:** [Zillow Research Data](https://www.zillow.com/research/data/) — ZHVI All Homes Mid-Tier  
**Geography:** California · Washington · Oregon · Nevada (1,406 cities)  
**Time span:** June 2015 – June 2025 (121 months)

---

## TL;DR

Ten years of Zillow Home Value Index data across 1,406 West Coast cities — cleaned, analyzed, and modeled to identify which market characteristics predict long-term appreciation. The West Coast median home value grew **77% between 2015 and 2025**, with wide dispersion driven by metro-level dynamics, COVID-era demand shocks, and rate sensitivity.

---

## Business Problem

Real estate investors, homebuyers, and policymakers need to understand **which West Coast markets are undervalued, which are overheated, and what structural factors drive long-term appreciation**. Raw ZHVI data answers "what happened" — this project answers "why" and "what's likely next."

---

## Dataset Overview

| Attribute | Detail |
|-----------|--------|
| Source | Zillow Research — ZHVI All Homes Mid-Tier |
| Geography | West Coast cities (CA, WA, OR, NV) |
| Rows | 1,406 cities |
| Time coverage | Jun 2015 – Jun 2025 (121 months) |
| ZHVI definition | Typical home value, 35th–65th percentile per city |
| Neural Zestimate | Full series upgraded Jan 2023 release |
| Missing values | 25 cities with sparse gaps (2019–2021); imputed via linear interpolation |

---

## Methodology

### Part 1 — Data Structuring & Cleaning
- Profiled raw wide-format data (1,406 × 128)
- Reshaped to long format: 170,126 city-month observations
- Imputed sparse ZHVI gaps using within-city linear interpolation
- Engineered: year/month/quarter, 1m/3m/12m lags, MoM % change, YoY % change, 3m rolling average, 10-year appreciation, volatility coefficient

### Part 2 — EDA & Feature Engineering *(in progress)*
- State and metro-level ZHVI comparisons
- COVID-era shock analysis (2020–2021)
- Appreciation distribution and outlier markets
- Correlation analysis for model feature selection

### Part 3 — Housing Price Predictor *(planned)*
- Predict ZHVI using lagged values, geographic features, and engineered signals
- Model evaluation: RMSE, MAE, R²
- Feature importance analysis

---

## Key Findings

*(To be completed after Part 2 EDA)*

---

## Tools & Libraries

| Tool | Purpose |
|------|---------|
| pandas | Data wrangling, reshape, feature engineering |
| numpy | Numerical operations |
| matplotlib + seaborn | Visualization |
| scikit-learn | Predictive modeling (Part 3) |
| pyarrow / parquet | Efficient storage of processed data |

---

## How to Run

```bash
# Clone and install
git clone https://github.com/DanielSantiagoGuzman/zillow-housing-analysis.git
cd zillow-housing-analysis
pip install -r requirements.txt

# Run notebooks in order
jupyter notebook part1_data_cleaning.ipynb
jupyter notebook part2_eda.ipynb          # coming
jupyter notebook part3_predictor.ipynb    # coming
```

> **Note:** The raw CSV is not tracked in git (see `.gitignore`). Download from [Zillow Research](https://www.zillow.com/research/data/) and place in `data/`. Processed parquets in `data/processed/` are tracked.

---

## Repository Structure

```
zillow-housing-analysis/
├── data/
│   ├── raw/                    # Raw CSV (not tracked)
│   └── processed/
│       ├── zhvi_long.parquet   # 170,126 city-month observations
│       └── city_snapshot.parquet  # 1,406 city summary stats
├── outputs/                    # Charts and exports
├── part1_data_cleaning.ipynb
├── part2_eda.ipynb             # Coming
├── part3_predictor.ipynb       # Coming
├── requirements.txt
├── MILESTONES.md
└── .gitignore
```
