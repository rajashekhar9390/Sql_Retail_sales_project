# Retail Sales Analysis SQL Project

## 📌 Project Overview

**Project Title**: Retail Sales Analysis
**Level**: Beginner SQL Project
**Database**: `sql_project_p1`

This project demonstrates practical SQL skills used in data analysis and data engineering to explore, clean, and analyze retail sales data. The project includes database creation, data cleaning, exploratory data analysis (EDA), and solving business problems using SQL queries.

This project helped improve my SQL querying, analytical thinking, and business problem-solving skills.

---

# 🎯 Objectives

1. Create and manage a retail sales database
2. Perform data cleaning and handle null values
3. Conduct exploratory data analysis (EDA)
4. Solve business-related business questions using SQL
5. Generate meaningful insights from retail sales data

---

# 🛠 Database Setup

## Create Database

```sql
CREATE DATABASE sql_project_p1;
```

## Create Table

```sql
CREATE TABLE retail_sales1
(
    transaction_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(20),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

---

# 🔍 Data Exploration & Cleaning

## Total Records

```sql
SELECT COUNT(*) FROM retail_sales1;
```

## Unique Customers

```sql
SELECT COUNT(DISTINCT customer_id) FROM retail_sales1;
```

## Unique Categories

```sql
SELECT DISTINCT category FROM retail_sales1;
```

## Null Value Check

```sql
SELECT *
FROM retail_sales1
WHERE
    transaction_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR customer_id IS NULL
    OR gender IS NULL
    OR category IS NULL
    OR quantity IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;
```

## Delete Null Records

```sql
DELETE FROM retail_sales1
WHERE
    transaction_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR customer_id IS NULL
    OR gender IS NULL
    OR category IS NULL
    OR quantity IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;
```

---

# 📊 SQL Questions & Answers

## Q1. Retrieve all sales made on '2022-11-05'

```sql
SELECT *
FROM retail_sales1
WHERE sale_date = '2022-11-05';
```

---

## Q2. Retrieve all Clothing transactions where quantity sold is more than 4 in Nov-2022

```sql
SELECT *
FROM retail_sales1
WHERE category = 'Clothing'
    AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
    AND quantity >= 4;
```

---

## Q3. Calculate total sales for each category

```sql
SELECT
    category,
    SUM(total_sale) AS net_sale,
    COUNT(*) AS total_orders
FROM retail_sales1
GROUP BY category;
```

---

## Q4. Find the average age of customers who purchased Beauty products

```sql
SELECT
    ROUND(AVG(age), 2) AS avg_age
FROM  retail_sales1
WHERE category = 'Beauty';
```

---

## Q5. Find all transactions where total_sale is greater than 1000

```sql
SELECT *
FROM retail_sales1
WHERE total_sale > 1000;
```

---

## Q6. Find total number of transactions made by each gender in each category

```sql
SELECT
    category,
    gender,
    COUNT(*) AS total_transactions
FROM retail_sales1
GROUP BY category, gender
ORDER BY category;
```

---

## Q7. Find the best selling month in each year based on average sales

```sql
SELECT
    year,
    month,
    avg_sale
FROM
(
    SELECT
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER(
            PARTITION BY EXTRACT(YEAR FROM sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rank
    FROM retail_sales1
    GROUP BY 1,2
) AS ranked_sales
WHERE rank = 1;
```

---

## Q8. Find the top 5 customers based on highest total sales

```sql
SELECT
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales1
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```

---

## Q9. Find the number of unique customers from each category

```sql
SELECT
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales1
GROUP BY category;
```

---

## Q10. Find shift-wise number of orders

```sql
WITH hourly_sales AS
(
    SELECT *,
        CASE
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales1
)

SELECT
    shift,
    COUNT(*) AS total_orders
FROM hourly_sales
GROUP BY shift;
```

---

# 📈 Key Insights

* Identified top-performing product categories
* Analyzed customer purchasing behavior
* Found monthly sales trends and peak sales periods
* Identified high-value customers and transactions
* Performed shift-wise order analysis

---

# 🚀 Skills & Technologies Used

* SQL
* PostgreSQL
* Data Cleaning
* Data Analysis
* Window Functions
* Common Table Expressions (CTE)
* Business Analysis

---

# 📂 Project Repository

👉 GitHub Repository:
https://github.com/rajashekhar9390

---

# 👨‍💻 Author

## Rajashekhar Kappa

☁️ GIS Engineer Exploring the World of Azure Data Engineering

🔗 LinkedIn:
https://www.linkedin.com/in/rajashekhar-kappa-5bb83b300

💻 GitHub:
https://github.com/rajashekhar9390

🏅 HackerRank:
https://www.hackerrank.com/profile/rajashekharkappa

📫 Email:
[rajashekharkappa@gmail.com](mailto:rajashekharkappa@gmail.com)

