📊 Retail Sales Analysis – SQL Project
📌 Project Overview

Project Title: Retail Sales Analysis
Database: Sql_project_1

This project demonstrates essential SQL skills and techniques commonly used by data analysts to explore, clean, and analyze retail sales data. The project covers database creation, data cleaning, exploratory data analysis (EDA), and answering real-world business questions using SQL.

This project is ideal for beginners who want to build a strong foundation in SQL and understand how SQL is applied in business scenarios.

🎯 Project Objectives

Set up a retail sales database

Perform data cleaning and handle missing values

Conduct exploratory data analysis (EDA)

Answer business-driven questions using SQL

Gain hands-on experience with aggregations, window functions, and CTEs

🗂 Project Structure
1️⃣ Database Setup

Database Creation
```sql

CREATE DATABASE Sql_project_1;
```


Table Creation

```sql
CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
); 
```

2️⃣ Data Exploration & Cleaning

Total Records

```sql
SELECT COUNT(*) FROM retail_sales; 
```


Unique Customers

```sql
SELECT COUNT(DISTINCT customer_id) FROM retail_sales; 
```


Unique Categories

```sql
SELECT DISTINCT category FROM retail_sales; 
```


Null Value Check

```sql
SELECT * 
FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR
    gender IS NULL OR age IS NULL OR category IS NULL OR
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL; 
```


Remove Records with Missing Data

```sql
DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR
    gender IS NULL OR age IS NULL OR category IS NULL OR
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```

📈 Data Analysis & Business Questions
🔹 Sales on a Specific Date
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05'; 
```

🔹 Clothing Transactions (Nov 2022, Quantity ≥ 4)
```sql
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
  AND DATE_FORMAT(sale_date, '%Y-%m') = '2022-11'
  AND quantity >= 4; 
```

🔹 Total Sales per Category
```sql
SELECT 
    category,
    SUM(total_sale) AS net_sale,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category; 
```

🔹 Average Age of Beauty Category Customers
```sql
SELECT 
    ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty'; 
```

🔹 High-Value Transactions (> 1000)
```sql
SELECT *
FROM retail_sales
WHERE total_sale > 1000; 
```

🔹 Transactions by Gender & Category
```sql
SELECT 
    category,
    gender,
    COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY category, gender
ORDER BY category; 
```

🔹 Best Selling Month in Each Year (Average Sale)
```sql
SELECT 
    year,
    month,
    avg_sale
FROM (
    SELECT 
        YEAR(sale_date) AS year,
        MONTH(sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER (
            PARTITION BY YEAR(sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rnk
    FROM retail_sales
    GROUP BY YEAR(sale_date), MONTH(sale_date)
) t
WHERE rnk = 1; 
```

🔹 Top 5 Customers by Total Sales
```sql
SELECT 
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5; 
```

🔹 Unique Customers per Category
```sql
SELECT 
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category; 
```

🔹 Sales Shift Analysis (Morning / Afternoon / Evening)
```sql
WITH hourly_sale AS (
    SELECT *,
        CASE
            WHEN HOUR(sale_time) < 12 THEN 'Morning'
            WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) AS total_orders
FROM hourly_sale
GROUP BY shift; 
```

🔍 Key Findings

Sales are distributed across multiple categories such as Clothing and Beauty.

A small group of customers contributes significantly to total revenue.

High-value transactions indicate premium purchasing behavior.

Certain months consistently perform better in terms of average sales.

Evening shifts record higher transaction volumes compared to other shifts.

📊 Reports Generated

Sales Summary Report – Category-wise and customer-wise performance

Trend Analysis – Monthly and yearly sales patterns

Customer Insights – Top customers and unique customer distribution

🧠 Learning Outcomes

Strong understanding of SQL aggregation and filtering

Practical use of window functions and CTEs

Improved ability to translate business questions into SQL queries

Experience with real-world retail sales data analysis

🛠 Tools Used

MySQL 8.0

SQL Workbench

GitHub

👤 Author

Anand Pathak
Aspiring Data Analyst
Skilled in SQL, Data Analysis, and Business Insights

📌 This project is part of my data analytics portfolio and showcases SQL skills essential for entry-level Data Analyst roles.
