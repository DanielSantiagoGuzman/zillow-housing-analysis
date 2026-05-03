# West Coast Housing Price Analysis & Predictor

**Tools:** Python · Pandas · Scikit-learn · Matplotlib · Seaborn · Parquet  
**Source:** [Zillow Research Data](https://www.zillow.com/research/data/): ZHVI All Homes Mid-Tier  
**Geography:** California · Washington · Oregon · Nevada (1,406 cities)  
**Time span:** June 2015 – June 2025 (121 months)

---

## TL;DR

Ten years of Zillow Home Value Index data across 1,406 West Coast cities, cleaned, analyzed, and modeled to identify which market characteristics predict long-term appreciation. The West Coast median home value grew **77% between 2015 and 2025**, with wide dispersion driven by metro-level dynamics, COVID-era demand shocks, and rate sensitivity.

---

## Business Problem

Real estate investors, homebuyers, and policymakers need to understand **which West Coast markets are undervalued, which are overheated, and what structural factors drive long-term appreciation**. Raw ZHVI data answers "what happened" — this project answers "why" and "what's likely next."

---

## Dataset Overview

| Attribute | Detail |
|-----------|--------|
| Source | Zillow Research: ZHVI All Homes Mid-Tier |
| Geography | West Coast cities (CA, WA, OR, NV) |
| Rows | 1,406 cities |
| Time coverage | Jun 2015–Jun 2025 (121 months) |
| ZHVI definition | Typical home value, 35th–65th percentile per city |
| Neural Zestimate | Full series upgraded Jan 2023 release |
| Missing values | 25 cities with sparse gaps (2019–2021); imputed via linear interpolation |

---

## Methodology

### Part 1: Data Structuring & Cleaning
- Profiled raw wide-format data (1,406 × 128)
- Reshaped to long format: 170,126 city-month observations
- Imputed sparse ZHVI gaps using within-city linear interpolation
- Engineered: year/month/quarter, 1m/3m/12m lags, MoM % change, YoY % change, 3m rolling average, 10-year appreciation, volatility coefficient

### Part 2: EDA & Feature Engineering
- State and metro-level ZHVI comparisons across the full 10-year window
- COVID-era shock analysis: lockdown pause, pandemic boom, rate-hike correction
- Appreciation distribution, outlier markets, and volatility-return tradeoff
- Seasonal pattern analysis and feature correlation matrix for model selection

### Part 3: Housing Price Predictor
- Three models trained on temporal split (train: Jun 2016–Dec 2023 · test: Jan 2024–Jun 2025)
- Ridge Regression (baseline) · Random Forest · Gradient Boosting
- Evaluation: MAE, RMSE, MAPE, R² with honest assessment of autoregressive dominance
- Feature importance analysis and residual diagnostics

---

## Key Findings

**Market trends (2015–2025)**
- West Coast median ZHVI grew **77%** over the decade, with CA leading at $460K → $865K.
- Washington secondary markets (Centralia, Olympia, Longview) were the top-appreciating metros, driven by Seattle-area spillover demand — up 117–124% in 10 years.
- All four states hit simultaneous YoY peaks of 20–26% in mid-2021, then all went negative by May 2023, the first synchronized correction since the post-GFC period.

**COVID impact**
- The initial lockdown (Mar–Sep 2020) froze inventory alongside demand; prices barely dipped.
- The 18-month pandemic boom (Jan 2021–Jun 2022) delivered what normally takes 5–7 years of appreciation.
- The Fed's 2022 rate hike cycle produced a cooling, not a crash; prices stayed well above pre-COVID levels in all four states.

**Model results**
- **Best model: Random Forest** — MAE $1,634 · MAPE 0.12% on 18-month holdout (Jan 2024–Jun 2025).
- Autoregressive lag features (1m lag, 3m rolling mean) explain >97% of predictive power.
- The hard problem is predicting inflection points — for that, exogenous data (mortgage rates, inventory, migration) is required.

---

## Tools & Libraries

| Tool | Purpose |
|------|---------|
| pandas | Data wrangling, reshape, feature engineering |
| numpy | Numerical operations |
| matplotlib + seaborn | Visualization |
| scikit-learn | Predictive modeling |
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
jupyter notebook part2_eda.ipynb
jupyter notebook part3_predictor.ipynb
```

> **Note:** The raw CSV is not tracked in git (see `.gitignore`). Download from [Zillow Research](https://www.zillow.com/research/data/) and place in `data/`. Processed parquets in `data/processed/` are tracked.

---

## Repository Structure

```
zillow-housing-analysis/
├── data/
│   ├── raw/                       # Raw CSV (not tracked)
│   └── processed/
│       ├── zhvi_long.parquet      # 170,126 city-month observations
│       └── city_snapshot.parquet  # 1,406 city summary stats
├── outputs/                       # Charts and exports
├── part1_data_cleaning.ipynb
├── part2_eda.ipynb
├── part3_predictor.ipynb
├── requirements.txt
├── MILESTONES.md
└── .gitignore
```
