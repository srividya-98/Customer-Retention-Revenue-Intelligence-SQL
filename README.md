# Customer Retention & Revenue Intelligence (SQL) — DuckDB

Pure **SQL-first** analytics on retail transactions using **DuckDB** (in-memory) inside a Jupyter Notebook.  
Goal: turn raw invoice lines into clean, analysis-ready sales data and answer core business questions on **revenue stability** and **customer retention**.

> Note: GitHub may label this repo as “Jupyter Notebook” because the main artifact is an `.ipynb`.  
> The analysis itself is performed using **SQL queries executed via DuckDB**.

---

## Business Question
**How can a retail business improve customer retention and revenue stability using historical transaction data?**

---

## Dataset
- Source: Kaggle — Online Retail Customer Clustering  
  https://www.kaggle.com/datasets/hellbuoy/online-retail-customer-clustering
- Raw rows loaded: **541,909**
- Analysis period (after parsing InvoiceDate): **2010-12-01 → 2011-12-09**
- Data file is **not committed** to GitHub (size + licensing).

---

## Tech Stack
- DuckDB (in-memory)
- SQL (CTEs, window functions, time-series aggregation)
- Python (only to run SQL + render outputs)

---

## Workflow (What the notebook does)
1. **Load & validate data**  
   - Load CSV into DuckDB table: `raw_data`
   - Confirm row count

2. **Clean transactions (create a reusable view)**  
   - Build `valid_sales` view:
     - exclude cancellations (`InvoiceNo NOT LIKE 'C%'`)
     - keep positive quantity and price (`Quantity > 0`, `UnitPrice > 0`)
   - Clean rows: **530,104**

3. **Core KPIs**
   - Total revenue (clean sales): **~10.67M**
   - Average Order Value (AOV): **~534.40** across **19,960 invoices**

4. **Trends**
   - Monthly revenue + order volume (seasonality)
   - Peak month: **Nov 2011** (highest revenue + order count)

5. **Product revenue concentration (Pareto-style)**
   - Rank products by revenue using window functions
   - Revenue is relatively diversified; top 20 contribute **~15%** of revenue
   - Operational line items (e.g., postage/manual) appear among top lines and should be excluded for “pure product” analysis

6. **Customer frequency segmentation (retention signal)**
   - Bucket customers by number of distinct orders:
     - **1 order:** 34.4%
     - **2–5 orders:** 45.5%
     - **6–10 orders:** 12.3%
     - **>10 orders:** 7.8%

---

## Key Insights (Executive Summary)
- Revenue shows strong seasonality, peaking in **November**, driven mainly by **higher order volume**.
- The product portfolio is **not overly concentrated**; revenue is spread across many SKUs.
- Some “revenue” comes from **operational charges** (postage/manual) and should be separated from product performance analysis.
- Customer base has a strong repeat component: **~65.6%** of customers placed **2+ orders**, indicating meaningful retention.
- The biggest retention opportunity is the **34%** of customers who purchased only once (churn risk).

---


