# predicting-house-values

## Overview
Raw dataset downloaded from [Zillow](https://www.zillow.com/research/data/) 
- The raw dataset is **not** included in this repository due to size. If you plan to rerun the preprocessing notebook, download the raw file using the link below and place it in the project root folder.
- **Data Type:** ZHVI All Homes (SFR, Condo/Co-op) Time Series, Smoothed, Seasonally Adjusted
- **Geography:** ZIP Code
- **Direct link:** [Download](https://files.zillowstatic.com/research/public_csvs/zhvi/Zip_zhvi_uc_sfrcondo_tier_0.33_0.67_sm_sa_month.csv?t=1744388430)

### Notes

- Data was trimmed to start from the first valid ZHVI entry per ZIP.
- All missing values were filled via linear interpolation within each ZIP's time series.
- Cutoff for feature data: `2024-02-29`
- Target prediction date: `2025-02-28`

## Processed Dataset Columns


| Column Name            | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `ZIP`                 | ZIP code                                                                     |
| `City`                | City name                                                                    |
| `Metro`               | Metro area name                                                              |
| `CountyName`          | County name                                                                  |
| `StateSizeRank`       | Rank of the ZIP within the state based on original size rank                 |
| `FinalZHVI`           | Home value as of the cutoff date (`2024-02-29`)                              |
| `FinalZScore`         | Z-score of the final ZHVI across all ZIPs in the state                       |
| `ZHVI_Tier`           | Tier assigned based on Z-score — one of: `very low`, `low`, `mid`, `high`, `very high` |
| `AvgYoYGrowth`        | Average year-over-year (YoY) growth (%)                                      |
| `MedianYoYGrowth`     | Median YoY growth (%)                                                        |
| `YoYGrowthVolatility` | Standard deviation of YoY growth (%)                                         |
| `NegativeGrowthYears` | Number of years with negative YoY growth                                     |
| `Total_Growth`        | Total percent growth over the trimmed ZHVI series                            |
| `CAGR`                | Compound annual growth rate over the full trimmed period (%)                 |
| `AvgMonthlyGrowth`    | Average monthly growth rate (%)                                              |
| `Volatility`          | Standard deviation of monthly growth (%)                                     |
| `2025-02-28`          | Target home value to be predicted (1 year after the cutoff)                  |



