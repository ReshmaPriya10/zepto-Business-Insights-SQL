# Zepto Business Insights SQL

This project analyzes a Zepto product dataset using SQL. It focuses on basic data exploration, lightweight cleaning, and business-style product analysis such as discounts, inventory availability, category revenue, and value-for-money comparisons.

## Project Files

- `Zepto_Business_Insights.sql` - table creation, cleaning steps, and analysis queries
- `zepto_v2.csv` - source dataset
- `LICENSE` - project license

## Project Overview

The SQL workflow in this project is organized into three parts:

1. Create a `zepto` table for product-level data
2. Explore and clean the dataset
3. Run analytical queries to answer common retail and inventory questions

The script is written in PostgreSQL-style SQL and uses data types such as `SERIAL`, `BOOLEAN`, and `NUMERIC`.

## Dataset Summary

Based on the CSV included in this repository:

- Total rows: `3732`
- Total categories: `14`
- In-stock products: `3279`
- Out-of-stock products: `453`

Example columns in the dataset:

- `category`
- `name`
- `mrp`
- `discountPercent`
- `availableQuantity`
- `discountedSellingPrice`
- `weightInGms`
- `outOfStock`
- `quantity`

## What The SQL Script Does

### 1. Table Creation

Creates a `zepto` table with fields for:

- product name and category
- original and discounted price
- stock availability
- product weight
- unit quantity

### 2. Data Exploration

The script checks:

- total number of rows
- sample records
- null values
- distinct categories
- stock vs out-of-stock counts
- duplicate product names across SKUs

### 3. Data Cleaning

The script performs two cleanup steps:

- removes products where `mrp = 0`
- converts `mrp` and `discountedSellingPrice` from paise to rupees

### 4. Data Analysis

The script answers these business questions:

1. Top 10 best-value products by discount percentage
2. High-MRP products that are out of stock
3. Estimated revenue by category
4. Products with MRP above 500 and discount below 10%
5. Top 5 categories with the highest average discount
6. Best price-per-gram products above 100g
7. Product grouping by weight: `Low`, `Medium`, `Bulk`
8. Total inventory weight by category

## How To Run

### Option 1: Run In PostgreSQL

Create the table first:

```sql
DROP TABLE IF EXISTS zepto;

CREATE TABLE zepto (
    sku_id SERIAL PRIMARY KEY,
    category VARCHAR(120),
    name VARCHAR(150) NOT NULL,
    mrp NUMERIC(8,2),
    discountPercent NUMERIC(5,2),
    availableQuantity INTEGER,
    discountedSellingPrice NUMERIC(8,2),
    weightInGms INTEGER,
    outOfStock BOOLEAN,
    quantity INTEGER
);
```

Load the CSV into PostgreSQL:

```sql
\copy zepto(category, name, mrp, discountPercent, availableQuantity, discountedSellingPrice, weightInGms, outOfStock, quantity)
FROM 'zepto_v2.csv'
WITH (FORMAT csv, HEADER true);
```

Then run the queries from [Zepto_SQL_data_analysis.sql](/d:/zepto-SQL-data-analysis-project/Zepto_SQL_data_analysis.sql).

### Option 2: Use The Script As A Reference

If you are practicing SQL in a learning environment, you can use the file as a query set for:

- PostgreSQL
- online SQL notebooks
- portfolio/demo SQL projects

You may need to adjust import syntax depending on the platform.

## Skills Demonstrated

- SQL table design
- filtering and sorting
- aggregation with `COUNT`, `SUM`, and `AVG`
- grouping with `GROUP BY`
- conditional logic with `CASE`
- data cleaning with `DELETE` and `UPDATE`
- business-focused exploratory analysis

## Notes

- The pricing fields in the raw dataset appear to be stored in paise, so the script converts them to rupees.
- The SQL file includes both exploratory and destructive cleaning statements. If you want to preserve the raw loaded table, create a backup before running the `DELETE` and `UPDATE` queries.
- One query comment contains a display issue for the rupee symbol. This does not affect execution logic, only the comment text.

## Future Improvements

- add visual dashboards in Power BI or Tableau
- create views for cleaned data and category-level summaries
- add advanced KPIs such as margin estimates or stock-risk scoring
- compare discount behavior across categories and pack sizes

## License

This project is available under the [MIT License](/LICENSE).
## Author
Reshma Priya Dayaka

## Skills Used
- SQL
- PostgreSQL
- Data Cleaning
- Data Analysis

## Key Insights
- Top revenue-generating categories
- Discount trend analysis
- Inventory availability analysis
- Product value-for-money comparison
