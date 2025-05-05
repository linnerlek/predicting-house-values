# ZIP-Level Home Value Growth Prediction

This project predicts next-year housing price growth by ZIP code in Georgia using Zillow ZHVI data and county-level ACS data.

## Overview

We construct a rolling, long-format dataset from 2011–2024 (excluding 2020) where each row represents a ZIP–year pair. Features are engineered from past ZHVI trends and ACS demographics. The target is the YoY percent growth from that year to the next.  

Final models were trained using Decision Tree, KNN, and Random Forest regressors. A tuned Random Forest using 16 selected features performed best.

## Data Sources

- **Zillow ZHVI**: Smoothed, seasonally adjusted home values by ZIP
- **ACS 1-Year Estimates**: Pulled from Census API at the county level  

Note: Raw files are not included. Place the downloaded ZHVI file in the project root to rerun the notebook.

## Features Used

- `FinalZHVI`, `AvgMonthlyGrowth`, `CAGR`, `Volatility`, `YoY_LastYear`, `NegativeGrowthYears`  
- ACS-based rates: poverty, education, unemployment, household size, age groups  
- One-hot encoded `Metro` and `CountyName` (rare values grouped as `Other`)  

Target: `YoY_target` = percent growth from current year to next year  

## Model Performance (Random Forest)

| Metric | Score |
|--------|-------|
| R²     | 0.774 |
| RMSE   | 2.32  |
| MAE    | 1.60  |
| SMAPE  | 36.1% |

Split was done by ZIP to prevent geographic leakage.

## Contributions

| Name           | Contributions               |
|----------------|-----------------------------|
| Linn Kloefta | All coding, analysis, report writing, and modeling |
