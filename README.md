# Vegetable Price & Sales Data Analysis

An end-to-end data cleaning and analysis project on about **2.76 million rows** of vegetable market price and sales data, built with **Databricks, PySpark and Delta tables**.

## Overview

Market price data is often messy: some records have negative quantities, or prices that do not make sense (for example, a minimum price higher than the maximum price). This project cleans such data, separates good records from bad ones, and builds summary tables that make price trends easy to analyze.

## Dataset

- **Size:** about 2.76 million rows (2,763,167 records)
- **Crops:** 19 vegetables
- **Period:** 1 Jan 2024 to 23 Sep 2026
- **Main columns:** date, market, crop name, minimum price, maximum price, modal price, quantity
- **Source:** [add the name or link of the data source here]
- **Price unit:** [add the unit here, for example ₹ per quintal]

## What I Did

1. **Cleaned the data**
   - Trimmed extra spaces in market and crop names
   - Checked every row for negative quantity
   - Checked every row for impossible prices (minimum greater than maximum, or modal price outside the minimum-maximum range)
   - Added `quality_issue` and `is_valid` columns to mark each row
2. **Silver table:** kept all 2,763,167 rows with a `quality_status` (VALID or INVALID)
3. **Gold table:** kept only the **2,761,217 valid rows** and added `year`, `month` and `price_spread` (maximum price minus minimum price)
4. **Summary tables**
   - Daily summary per crop (18,938 rows): average minimum, maximum and modal price, average and total quantity, average price spread
   - Monthly summary per crop: average prices, average quantity and number of observations
5. **Visualized** the daily average modal price trend for tomato

## Data Quality Results

| Check | Rows |
|---|---|
| Total rows (silver) | 2,763,167 |
| Valid rows (gold) | 2,761,217 |
| Invalid rows excluded | 1,950 |
| - Invalid price relationship | 1,946 |
| - Negative quantity | 4 |

## Key Finding (Tomato)

- Highest average modal price: **64.19** on **20 June 2024**
- Lowest average modal price: **11.80** on **27 March 2025**
- Prices were very unstable, with sharp spikes and drops. The highest price was about **5 times** the lowest.
- Spikes appeared in mid-2024 and late 2025, but they did not fall in the same month each year.

<img width="1512" height="805" alt="image" src="https://github.com/user-attachments/assets/986652e2-5a04-4524-89ed-5f283195709c" />

## Tables Created

| Layer | Table | Description |
|---|---|---|
| Silver | `silver_market_prices` | All cleaned rows with a quality status |
| Gold | `gold_market_prices` | Valid rows only, with year, month and price spread |
| Gold | `gold_daily_crop_summary` | Daily averages per crop |
| Gold | `gold_monthly_crop_summary` | Monthly averages per crop |

## Tools

Databricks, PySpark, Delta Lake, Python

## Repository Contents

- `vegetable_price_analysis.ipynb`: the full notebook (cleaning, silver and gold tables, summaries and the tomato chart)

## How to Run

1. Create a free Databricks workspace.
2. Import `vegetable_price_analysis.ipynb`.
3. Load your raw price data into a table and update the table names in the notebook.
4. Run the cells from top to bottom.

## Limitations and Next Steps

- Add a price comparison across all 19 vegetables (most stable and most unstable)
- Add a dashboard with trend charts per vegetable
- Add a forecast of future prices

## Author

**Harsith S J**
Final-year B.Tech Artificial Intelligence & Data Science student
GitHub: [S-harsith](https://github.com/S-harsith)
