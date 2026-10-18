# Customer Retention, Lifecycle and Segmentation Analysis for an E-commerce Business

A product analytics project on two years of transactions from a UK online gift wholesaler. It measures how many new customers come back, how quickly they return, which customers are at risk of churning, what a new customer is worth in their first year, and which segments drive revenue.

## Business questions
1. How many new customers come back, and how quickly does retention decay?
2. How long does it take a new customer to make a second purchase?
3. How many customers have gone quiet, and who are they?
4. How much is a new customer worth in their first year?
5. How concentrated is revenue, and which customer segments matter most?
6. Do markets (countries) behave differently?

## Key findings
- **About 1 in 5 new customers return the following month.** Month-1 retention is 21.0% for new-customer cohorts and decays slowly to about 14% by Month 11.
- **The second purchase is slow.** 40.8% of new customers buy again within 90 days; among those who return, the median wait is 73 days.
- **The business is strongly seasonal.** October to December produced 33% of 2010 revenue.
- **57% of eligible customers have not bought in the last 90 days.** About 1,680 of them are lapsed repeat buyers (43% of all repeat buyers).
- **A new customer is worth about £1,434 in their first 12 months.** Including the legacy cohort would inflate this to £2,197.
- **Revenue is highly concentrated.** The top 10% of customers generate 63.5% of revenue; Champions are 27% of customers and 74% of revenue.
- **117 high-value customers have lapsed** (no purchase in 180+ days), representing £933k of historical revenue.
- **Country differences are not statistically meaningful** (95% confidence intervals overlap).

## Recommendations
1. Protect the Champions segment: monitor purchase gaps and flag customers who go quiet.
2. Win back the 117 lapsed high-value customers with personal account-manager outreach.
3. A/B test an early repeat-purchase nudge around day 30-45 for new customers, with a randomized holdout group.
4. Run a separate, lower-cost re-engagement test for the wider 90-day-inactive group.
5. Investigate the acquisition slowdown (new customers fell from 250-440 to about 70-180 per month).
6. Run treatment and control groups in the same weeks so seasonality does not distort test results.

## Techniques
- **Cohort analysis:** monthly acquisition cohorts, a retention heatmap and customer-weighted retention curves
- **Bias control:** handling left-censoring (a legacy cohort of pre-existing customers) and right-censoring (cohorts not yet observable), plus fixed observation windows
- **Seasonality diagnosis:** separating calendar effects from lifecycle effects
- **Repeat purchase behavior:** time to second purchase and a cumulative return curve
- **Churn risk:** a 90-day inactivity proxy with an eligibility rule
- **Customer value:** 12-month LTV proxy per acquired customer; mean vs median for skewed spend
- **Revenue concentration:** top 1% / 10% share, with a net-of-returns sensitivity check
- **Segmentation:** RFM scoring with fixed, tie-safe thresholds and mutually exclusive segments
- **Statistical inference:** 95% Wilson confidence intervals for proportions
- **Experiment design:** recommendations framed as randomized holdout tests

| Column | Description |
|---|---|
| Invoice | Invoice number; numbers starting with 'C' are cancellations |
| StockCode | Product code |
| Description | Product name |
| Quantity | Units per line; negative values are returns |
| InvoiceDate | Date and time of the invoice |
| Price | Unit price (GBP) |
| Customer ID | Customer identifier (missing for about 23% of rows) |
| Country | Customer's country |

**Data preparation:** kept identified customers and non-cancelled product lines with quantity and price above zero; removed exact duplicates, non-product codes (postage, fees, adjustments, tests) and the incomplete month of December 2011. 71% of rows were kept, covering 5,824 customers.

## Project structure
```
├── retention_lifecycle_analysis.ipynb   # Full analysis
├── requirements.txt
└── README.md
```

## Limitations
- The data covers purchases only (no browsing, cart or campaign data), so findings are descriptive, not causal.
- Rows without a Customer ID (23%) are excluded, so results describe identified customers only.
- Revenue is gross sales, not profit.
- 90-day inactivity is a proxy for churn, not confirmed churn.
- Two years of data include only two holiday seasons.
