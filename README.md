# 🛒 E-Commerce Product Engagement & Conversion Analysis

## 📊 Project Overview
This project turns ⟦N⟧ million raw clickstream events (Oct–Nov 2019) into a compact, category-level reporting table in PostgreSQL, then visualizes it in an interactive Tableau dashboard. Cleaning and aggregation happen upstream in SQL, which keeps the dashboard fast and the logic reproducible.

| At a glance | |
|---|---|
| Source data | Kaggle eCommerce Behavior Data (multi-category store) |
| Raw events | ⟦N⟧ million rows |
| Summary table | 7,625 rows (day × product category) |
| Row reduction | ⟦computed from N⟧ (>99.9%) |
| Period | Oct 1 – Nov 30, 2019 |

## 🛠️ Tech Stack & Architecture
- **Database:** PostgreSQL 15 (Homebrew)
- **SQL IDE:** DBeaver Community Edition
- **Visualization:** Tableau Public
- **SQL techniques:** `SPLIT_PART()`, `INITCAP()`, `REPLACE()`, `CASE WHEN` conditional aggregation, `GROUP BY` / `HAVING`, a mapping table with `JOIN`

```
Kaggle CSVs → raw_events → product_performance_summary ─┐
 (Oct, Nov)   (PostgreSQL)   (day × category, cleaned)   ├→ Tableau
                              category_map (8 types) ────┘
```

## 📐 Data Transformation & Optimization
Raw category values are dot-separated paths (for example `furniture.universal.light`). Parsing millions of these inside Tableau caused rendering lag, so the work moved into SQL:

- **String cleaning:** `SPLIT_PART()`, `INITCAP()` and `REPLACE()` turn paths into readable labels (`Universal Light`).
- **Session-level aggregation:** ⟦describe your method, e.g. distinct sessions per day and category that reached view, cart and purchase, using conditional aggregation⟧.
- **Pre-aggregation:** collapsed ⟦N⟧ million events into a 7,625-row summary table, so Tableau reads a small table instead of raw logs.
- **Product-type grouping:** a `category_map` table maps ~130 categories into 8 product types (Phones & Computing, TV Audio & Camera, Kitchen Appliances, and so on). Changing a category's type is one row update, with no workbook edits.

## 📈 Key Findings
### 💰 Smartphones dominate revenue
Smartphones account for about **⟦X⟧%** of top-10 category revenue (`$334.8M` of `$⟦T⟧M`). At the product-type level, Phones & Computing leads with ⟦share⟧% of revenue.

👉 **[Open the interactive dashboard on Tableau Public](⟦your URL⟧)**

![Dashboard](images/dashboard.png)

### 🔻 Funnel
Of ⟦views⟧ product views, ⟦carts⟧ reached a cart (⟦x⟧%) and ⟦purchases⟧ ended in a purchase (⟦y⟧% of carts).

### 💡 Recommendation (a hypothesis to test)
Cart abandonment is ⟦confirm with the funnel numbers: the largest drop among users showing buying intent⟧, so a cart-reminder A/B test is a sensible next step. *Illustrative sizing:* recovering 2% of abandoned carts at an average order value of `$⟦AOV⟧` is about `$⟦Y⟧M`. This is a scenario, not a forecast.

## 🚧 Assumptions & Limitations
- Two months of data only: no seasonality and no true lifetime value.
- No order ID, so orders are approximated by purchase sessions.
- A session that touches several categories is counted in each, so category totals overlap.
- Sessions with no category were excluded from the summary. The `Uncategorized` bucket is excluded from rankings and totals on the dashboard.
- Revenue figures use ⟦Gross Revenue / Revenue Floor⟧.
- Product types are my own grouping, not part of the source data.

## ▶️ How to Reproduce
1. Download the two CSV files from Kaggle.
2. Create the database and load them into `raw_events`.
3. Run `transform_and_aggregate.sql` to build `product_performance_summary`.
4. Run `category_map.sql` to create the product-type mapping.
5. Connect Tableau to the summary table and join `category_map` on category.

## 🔗 Deliverables
- [SQL transformation script](sql/transform_and_aggregate.sql)
- [Category mapping script](sql/category_map.sql)
- Dashboard screenshots in `images/`
- Data source: [Kaggle eCommerce Behavior Data](⟦link⟧)
