# E-Commerce Product Engagement & Conversion Analysis

## Overview
Transformed [N] million clickstream events (Oct–Nov 2019, Kaggle
"eCommerce behavior data from multi-category store") in PostgreSQL into a
daily category-level summary table (7,625 rows) powering a Tableau Public dashboard.

## Tech Stack
PostgreSQL 15 · DBeaver · Tableau Public
SQL used: `SPLIT_PART`, `INITCAP`, `REPLACE`, `CASE WHEN` conditional aggregation,
`GROUP BY`, [CTEs / window functions, only if used]

## Approach
1. **Cleaned category paths in SQL.** Turned `furniture.universal.light` into
   `Universal Light` so Tableau doesn't parse strings row by row.
2. **Aggregated to sessions.** Counted sessions per day and category that reached
   view, cart and purchase. [Describe your method.]
3. **Pre-aggregated.** [N]M events → 7,625 rows (>99.9% fewer), so the
   dashboard responds quickly.

## Findings
- **Smartphones drive revenue:** about [88]% of top-10 category revenue.
  ![Revenue by category](images/revenue_by_category.png)
- **Cart → purchase is the biggest drop:** [X]% of cart sessions end without a purchase
  (excluding Nov 14–17). Highest in [category].

## Recommendation (hypothesis to test)
Cart abandonment is the largest funnel loss, so a cart-reminder A/B test is a reasonable
next step. Illustrative sizing: recovering 2% of abandoned carts at an average order value
of $[X] ≈ $[Y]. This is a scenario, not a forecast.

## Assumptions & Limitations
- Two months of data, so no seasonality or true lifetime value.
- No order ID, so orders are approximated by purchase sessions.
- Sessions that touch several categories are counted in each, so category totals overlap.
- Sessions with no category were excluded.

## Deliverables
- [SQL transformation script](transform_and_aggregate.sql)
- Dashboard screenshots are in the Findings section above.
- Data: Kaggle (check the dataset's license before sharing anything beyond aggregates).
