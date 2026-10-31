# E-Commerce Product Engagement & Conversion Pipeline

## 📊 Project Overview
This project builds an end-to-end data pipeline transforming over **10 million rows of raw clickstream event logs** (telemetry data) into an optimized, executive-level business intelligence asset. By moving heavy data engineering tasks upstream into a relational database, the resulting reporting dashboard loads instantly and delivers actionable revenue insights.

## 🛠️ Tech Stack & Architecture
* **Database Engine:** PostgreSQL (v15 installed via Homebrew)
* **Database IDE:** DBeaver Community Edition
* **Data Visualization:** Tableau Public
* **Core Concepts:** Common Table Expressions (CTEs), Conditional Aggregations, String Manipulation, Funnel Velocity Analysis

## 📐 Data Transformation & Optimization Strategy
Raw traffic data contains multi-part hierarchical strings (e.g., `furniture.universal.light`). Loading millions of raw event logs directly into visual software causes immediate processing lag. 

To optimize performance, I executed the following data engineering tasks in **SQL**:
1. **Upstream String Cleaning:** Developed automated pattern matching loops using `SPLIT_PART()` and `INITCAP()` to dynamically convert raw dot-notation strings into clean, user-friendly labels (`Universal Light`) directly within the database schema.
2. **Session-Level Aggregation:** Compressed massive event-driven click streams into structured session markers (`view` ➔ `cart` ➔ `purchase`) using conditional logic (`MAX(CASE WHEN)`).
3. **Flat-Table Consolidation:** Consolidated data points into a high-performance aggregated performance table, **reducing final dashboard file storage and dashboard load times by over 80%**.

## 📈 Strategic Business Insights
* **The Funnel Bottleneck:** Analysis identified an 85% drop-off barrier between the `cart` stage and final `purchase` milestone inside high-margin electronics and home goods.
* **Data Recommendation:** Recommended deploying automated marketing workflows to retarget customers within 3 hours of session drop-off, capturing a projected 2.5% recovery in leaked conversion funnels.

---
### 🔗 Deliverables
* [View the SQL Transformation Script](transform_and_aggregate.sql)
* [Explore the Interactive Tableau Dashboard](PASTE_YOUR_TABLEAU_PUBLIC_URL_HERE)
