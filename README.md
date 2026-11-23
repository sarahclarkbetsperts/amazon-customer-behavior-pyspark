# Amazon Customer Behavior Analysis (PySpark)

Analysis of **1.85 million Amazon purchase records (2018 onward)** joined to survey demographics, built with PySpark. The project covers data cleaning, exploratory analysis, RFM + K-Means customer segmentation, and business recommendations on promotions, retention, geography and inventory.

> Coursework project from my MS in Applied Data Science (UpGrad × IIIT Bangalore), big data module.

## Highlights

- **Scale:** 1,850,717 rows after joining purchases to survey responses on `Survey ResponseID`; 11,695 duplicates removed.
- **Seasonality:** November (10.1%) and December (10.5%) are the strongest months by revenue; Monday is the strongest weekday.
- **Segmentation:** RFM features (log-transformed, standardised) clustered with K-Means. k = 4 chosen from the WCSS elbow.
- **Concentration:** a small, highly active group (the "Champions" cluster, 21.6% of customers, average spend $11,609) drives most revenue.
- **Retention:** only 53.9% of customers bought on more than one day.
- **Fraud screen:** a simple mean + 3 SD rule ($171.70) flags 20,437 transactions (1.1%) for review.

## Customer segments

| Segment | Customers | Avg recency (days) | Avg frequency | Avg spend |
| --- | --- | --- | --- | --- |
| Champions | 3,466 (21.6%) | 585 | 414 | $11,609 |
| Regular buyers | 1,926 (12.0%) | 654 | 45 | $1,519 |
| Recent low-value | 5,355 (33.3%) | 806 | 1.3 | $66 |
| Lapsed one-timers | 5,324 (33.1%) | 1,604 | 1.2 | $66 |

## What's in the analysis

1. **Data preparation:** joins, missing-value handling, feature engineering (year, month, weekday, weekend flag, revenue = price × quantity)
2. **EDA:** purchase trends, weekday vs weekend, demographics vs frequency, co-purchased product pairs, top products, state-level patterns, price vs quantity, spend KPIs, seasonality
3. **RFM segmentation:** Recency, Frequency, Monetary features and K-Means clustering
4. **Business insights:** promotion timing, repeat purchases, fraud flags, demand volatility by category, bulk purchases, product lifecycle cohorts

## Repository structure

```
├── Customer_Behavior_Analysis.ipynb   # full PySpark notebook with outputs
├── reports/
│   └── Customer_Behaviour_Analysis_Report.pdf   # written summary of findings
└── README.md
```

## Tech stack

Python, PySpark (DataFrame API, window functions), scikit-learn (K-Means, StandardScaler), pandas, matplotlib, seaborn. Developed in Google Colab.

## Data

The notebook expects three CSV files: `amazon-purchases.csv`, `survey.csv` and `fields.csv`. They are **not included** in this repository because of their size and because they contain real purchase histories. The data appears to come from the open Amazon purchase-history dataset published on Harvard Dataverse; see its page for access and licence terms. [Add the dataset link here.]

To run the notebook, place the three files in `/content/` (or change the paths in the "Loading the Datasets" cell) and run all cells.

## Limitations

- Some CSV rows are misaligned (for example `Survey ResponseID` values such as "Metro"), which inflates the customer count to 16,071 against about 5,000 survey users. The two low-value clusters are mostly these one-purchase records, so spend-per-customer and RFM figures are distorted.
- One stray 2024 record sets the latest date to 2024-08-15, overstating recency for everyone.
- `Order Date` has no time of day, so the hourly analysis was replaced with day of month.
- `dropDuplicates()` may remove genuine repeat purchases, and the fraud rule is only a screen, not proof of fraud.

**Next step:** re-run the segmentation after removing the malformed rows.

## Author

**Sapna Bhayal**, Solution Architect | Backend & Data
[LinkedIn](add-your-url) · [GitHub profile](https://github.com/add-your-username)
