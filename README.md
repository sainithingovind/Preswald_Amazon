# 🏍️ Amazon Product Insights Dashboard

This dashboard provides an interactive interface to explore product ratings, categories, and review statistics from an Amazon product dataset using Preswald — a no-code/low-code platform for building data-driven apps.

---

## 🚀 Features

- **Interactive Filters**  
  - Slider to filter products by minimum rating  
  - Cleaned dataset using pandas and displayed with tables and charts

- **SQL & Python Integration**  
  - SQL preview queries run directly on CSV using DuckDB engine
  - Python-powered data cleaning and visualizations

- **Data Visualizations**  
  - 📊 Top-rated products (filtered by rating)  
  - 📈 Average rating by category  
  - 🧮 Most reviewed products (via SQL)  
  - 📦 Product count per category (SQL + chart)

---

## 📂 Dataset

- File: `amazonn.csv`
- Columns used:
  - `product_name`
  - `rating`
  - `rating_count`
  - `category`

---

## 🔍 Technologies

- **Preswald SDK**: `text()`, `table()`, `slider()`, `plotly()`, `query()`, `get_df()`
- **Plotly Express**: For interactive bar charts
- **pandas**: For data cleaning and transformations

---

## ✅ How to Run

1. Upload your `amazonn.csv` into the `/data` folder  
2. Ensure your `preswald.toml` includes:

```toml
[data.amazonn_csv]
type = "csv"
path = "data/amazonn.csv"
```

3. Run the app locally:

```bash
preswald run
```

---

## 📌 File Overview

| File           | Purpose                              |
|----------------|--------------------------------------|
| `hello.py`     | Main dashboard logic and UI layout   |
| `amazonn.csv`  | Source dataset (under `/data`)       |
| `preswald.toml`| Dataset configuration file           |

---

## 📊 Sample SQL Queries

```sql
-- Preview top 5 products
SELECT product_name, rating, category FROM amazonn_csv LIMIT 5;

-- Most reviewed products
SELECT product_name, rating_count 
FROM amazonn_csv 
WHERE rating_count IS NOT NULL 
ORDER BY CAST(REPLACE(rating_count, ',', '') AS INT) DESC 
LIMIT 10;

-- Product count per category
SELECT category, COUNT(*) AS product_count 
FROM amazonn_csv 
WHERE category IS NOT NULL 
GROUP BY category 
ORDER BY product_count DESC 
LIMIT 10;
```

---


