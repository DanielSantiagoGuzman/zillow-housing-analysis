# Project Milestones

## zillow-housing-analysis

| Date | Milestone |
|------|-----------|
| 2026-05-02 | Part 1 complete — data profiled, reshaped wide→long, cleaned, 9 features engineered, parquets exported |
| 2026-05-02 | Part 2 complete — 8 EDA charts, COVID shock analysis, metro appreciation rankings, seasonality, feature correlation |
| 2026-05-02 | Part 3 complete — Ridge, Random Forest, Gradient Boosting trained; RF best MAE $1,634 MAPE 0.12% on 18-month holdout |

---

## Notes
- Raw data: 1,406 West Coast cities × 121 months (Jun 2015 – Jun 2025)
- Source: Zillow Research ZHVI, All Homes Mid-Tier, neural Zestimate-upgraded series
- 25 cities had sparse ZHVI gaps (2019–2021); imputed via linear interpolation within each city's time series
- Processed files: `data/processed/zhvi_long.parquet` (170,126 rows), `data/processed/city_snapshot.parquet` (1,406 rows)
