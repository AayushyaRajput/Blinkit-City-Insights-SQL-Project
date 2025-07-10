# Blinkit-City-Insights-SQL-Project
📊 SQL project to estimate item-level sales across Indian cities using Blinkit’s scraped inventory data. Analyzed inventory fluctuations using window functions, joined category and location mappings, and created a clean insights table for business reporting.

This project involves writing complex SQL queries to derive meaningful insights from Blinkit SKU inventory data. The goal is to estimate the quantity of items sold across cities using inventory movement over time.

## 📊 Objective

To create a derived table named `blinkit_city_insights` that:
- Integrates data from 3 base tables:
  - `all_blinkit_category_scraping_stream`
  - `blinkit_categories`
  - `blinkit_city_map`
- Estimates quantity sold (`est_qty_sold`) for each SKU based on changes in inventory over time.

---

## 📁 Dataset Description

Raw CSVs provided (imported into MySQL):
- `all_blinkit_category_scraping_stream.csv` – Inventory snapshots at different timestamps
- `blinkit_categories.csv` – Category & subcategory mappings
- `blinkit_city_map.csv` – Store to city mapping

Each record in the final output contains:
- `date_time`
- `city_name`
- `category_name`
- `subcategory_name`
- `sku_id`
- `store_id`
- `total_est_qty_sold`

---

## ⚙️ Tools Used

- MySQL 8+
- MySQL Workbench
- SQL (CTE, window functions, joins)
- CSV export

---

## 🔍 Approach

- Used the `LEAD()` window function to compare inventory values across consecutive timestamps.
- Calculated estimated quantity sold as the difference between current and next inventory.
  - If inventory dropped, the difference was counted as `est_qty_sold`.
  - If inventory increased, it was treated as a restock (and sale = 0).
- Joined with category and city tables to enrich data.

---

## 🧪 Sample Output

| date_time          | city_name | category_name | subcategory_name   | sku_id | store_id | total_est_qty_sold |
|--------------------|-----------|----------------|---------------------|--------|----------|---------------------|
| 06-03-2025 01:13   | Agra      | Munchies       | Bhujia & Mixtures   | 559017 | 33920    | 1                   |
| 06-03-2025 01:13   | Agra      | Munchies       | Bhujia & Mixtures   | 547731 | 33920    | 2                   |

---

## 📦 Files in This Repo

- `blinkit_city_insights_query.txt` – Final SQL query
- `blinkit_city_insights.csv` – Output data exported from MySQL

---

## ✅ How to Run

1. Create a MySQL database (e.g. `blinkit_data`)
2. Import the provided CSVs into MySQL tables using Workbench
3. Run the query in `blinkit_city_insights_query.txt`
4. Export results as `blinkit_city_insights.csv`
