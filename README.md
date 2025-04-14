# predicting-house-values

## Overview
Raw dataset downloaded from [Zillow](https://www.zillow.com/research/data/) 
- The raw dataset is **not** included in this repository due to size. If you plan to rerun the preprocessing notebook, download the raw file using the link below and place it in the project root folder.
- **Data Type:** ZHVI All Homes (SFR, Condo/Co-op) Time Series, Smoothed, Seasonally Adjusted
- **Geography:** ZIP Code
- **Direct link:** [Download](https://files.zillowstatic.com/research/public_csvs/zhvi/Zip_zhvi_uc_sfrcondo_tier_0.33_0.67_sm_sa_month.csv?t=1744388430)

### Notes

- Data was trimmed to start from the first valid ZHVI entry per ZIP.
- All missing values within the time series were filled using linear interpolation.
- The cutoff date for feature data is **`2024-02-29`**.
- The target variable is **`YoY_2025`**, representing the year-over-year percent growth between `2024-02-29` and `2025-02-28`.
- ZIPs with incomplete or insufficient data were removed after interpolation.
- `City` was excluded from the final dataset due to high fragmentation and low predictive value.

## Processed Dataset Columns

These are the columns in the final processed dataset used for modeling.

| Column Name            | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `ZIP`                 | ZIP code                                                                     |
| `Metro`               | Metro area name (filled using city/county mapping where missing)             |
| `CountyName`          | County name                                                                  |
| `StateSizeRank`       | Rank of the ZIP within the state based on original size rank                 |
| `FinalZHVI`           | Home value as of the cutoff date (`2024-02-29`)                              |
| `FinalZScore`         | Z-score of the final ZHVI across all ZIPs in the state                       |
| `ZHVI_Tier`           | Tier assigned based on Z-score — one of: `very low`, `low`, `mid`, `high`, `very high` |
| `YoY_2001`–`YoY_2024` | Year-over-year (YoY) growth rates (%) from 2001 to 2024                      |
| `AvgYoYGrowth`        | Average YoY growth (%) across available years                                |
| `MedianYoYGrowth`     | Median YoY growth (%)                                                        |
| `YoYGrowthVolatility` | Standard deviation of YoY growth (%)                                         |
| `NegativeGrowthYears` | Number of years with negative YoY growth                                     |
| `YoY_2025`            | **Target**: Projected YoY growth from `2024-02-29` to `2025-02-28` (%)       |
