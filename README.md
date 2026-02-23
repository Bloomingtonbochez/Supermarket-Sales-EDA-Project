# Supermarket-Sales-EDA-Project
This project presents a comprehensive end-to-end SQL exploratory data analysis (EDA) of the popular Supermarket Sales dataset (Kaggle), containing 1,000 retail transactions across multiple branches and cities.  The objective of this project was to transform raw transactional data into actionable business intelligence using advanced SQL techniques.
## 📌 Project Overview

This repository demonstrates **intermediate-to-advanced SQL skills** applied to real-world retail data. Using the popular **Supermarket Sales** dataset from Kaggle, I performed exploratory data analysis (EDA) to answer key business questions such as:

- Which branches and cities generate the most revenue?
- What product lines are most profitable and highly rated?
- When (time/day/month) do peak sales occur?
- How do customer types (Member vs Normal), gender, and payment methods influence spending?
- Which segments show price sensitivity or outlier behavior?
- Pareto / MoM growth / ranking insights for strategic decisions

The project focuses purely on **SQL** (no Python/Power BI here) to showcase clean, readable, and performant queries using window functions, CTEs, date functions, ranking, and business logic

# 🎯 Objectives

- Perform data quality checks and basic exploration 
- Answer business-oriented questions via SQL
- Use advanced SQL features like CTEs, window functions, LAG, NTILE
- Derive actionable insights and recommendations

## 📊 Dataset

- **Source**: [Supermarket Sales on Kaggle](https://www.kaggle.com/datasets/aungpyaeap/supermarket-sales)
- **Rows**: 1,000 transactions
- **Time period**: Jan–Mar 2019
- **Branches**: 3 (A, B, C) in 3 cities (Yangon, Mandalay, Naypyitwa)
- **Key columns**: Invoice ID, Branch, City, Customer type, Gender, Product line, Unit price, Quantity, Total, Date, Time, Payment, gross income, Rating

**No missing values** — clean in MS EXCEL making the dataset is clean and ready for analysis 
## 🛠️ Technologies & Tools

- **Database**: SQLserver for Analysis (queries are mostly standard SQL)
- **clean**: Ms Excel

# 📊 SQL Exploratory Data Analysis – Question Flow (Basic → Advanced)

## 🟢 1. Dataset Overview

1. What is the total number of transaction rows in the dataset?

2. How many unique branches/cities are there, and what is the total sales amount per branch?
 ```sql
SELECT
COUNT(DISTINCT branch)total_branches,
COUNT(DISTINCT city) total_cities
FROM supermarket_sales
SELECT
    branch,
    city,
    ROUND(SUM(sales_amount), 2) AS total_sales
FROM (
    SELECT 
        branch,
        city,
        ([unit_cost] * Quantity) AS sales_amount
    FROM supermarket_sales
) AS derived
GROUP BY branch, city
ORDER BY total_sales DESC
```

## 🟡 2. Revenue & Product-Level Aggregation

3. What is the total revenue generated overall and broken down by product line/category?
```SELECT 
    product_line,
    ROUND(SUM(revenue), 2) AS total_revenue
FROM supermarket_sales
GROUP BY product_line
ORDER BY total_revenue DESC
```

5. What is the total revenue and quantity sold by Product line? Rank the product lines from highest to lowest revenue.

6. Which product line has the highest total quantity sold?
```
WITH qty_cte AS (
    SELECT 
        product_line,
        SUM(quantity) AS quantity_sold,
        RANK() OVER (ORDER BY SUM(quantity) DESC) AS rnk
    FROM supermarket_sales
    GROUP BY product_line
)
SELECT product_line, quantity_sold
FROM qty_cte
WHERE rnk = 1;
```
6. Which product line has the highest average unit price?
```SELECT TOP 1
    product_line,
    ROUND(AVG(unit_cost), 2) AS avg_unit_price
FROM supermarket_sales
GROUP BY product_line
ORDER BY avg_unit_price DESC
```

## 🟠 3. Advanced Product Metrics

7.  Which product line has the highest average spend per transaction?
   ```SELECT TOP 1
    product_line,
    ROUND(
        SUM(revenue) * 1.0 / COUNT(DISTINCT invoice_id),
    2) AS avg_spend_per_transaction
FROM supermarket_sales
GROUP BY product_line
ORDER BY avg_spend_per_transaction DESC
```
--For each Product line, what is the average Unit price and average Quantity purchased? 
```SELECT TOP 1
    product_line,
    SUM(quantity) AS quantity_sold
FROM supermarket_sales
GROUP BY product_line
ORDER BY quantity_sold DESC
```

---

## 🔵 4. Customer & Gender Analysis

8. What is the distribution of customer types — count and percentage of total sales?
```SELECT 
    customer_type,
    COUNT(*) AS total_transactions,
    SUM(unit_price * quantity) AS total_sales,
    ROUND(
        SUM(unit_price * quantity) * 100.0 
        / SUM(SUM(unit_price * quantity)) OVER(), 
    2) AS sales_percentage
FROM supermarket_sales
GROUP BY customer_type
ORDER BY total_sales DESC;
```

9. How do sales differ by gender? Which gender contributes more to revenue in each product line?
```sql
WITH cte_revenuebygender AS (
    SELECT 
        product_line,
        gender_customer,
        ROUND(SUM(revenue),2) AS total_revenue,
        ROW_NUMBER() OVER (PARTITION BY product_line ORDER BY SUM(revenue) DESC) AS RN
    FROM supermarket_sales
    GROUP BY product_line, gender_customer
)
SELECT 
    product_line,
    gender_customer,
    total_revenue
FROM cte_revenuebygender
WHERE RN = 1;
```
---

## 🟣 5. Time-Based Analysis

11. Extract the month and day of week from the Date column. Which month has the highest total sales? Which day of the week is busiest?
```
SELECT TOP 1
    DATENAME(WEEKDAY, date) AS Day_Name,
    ROUND(SUM(unit_price * quantity), 2) AS total_sales
FROM supermarket_sales
GROUP BY DATENAME(WEEKDAY, date)
ORDER BY total_sales DESC
```

---

## 🔴 6. Branch & City Performance (Advanced KPIs)

12. Calculate total sales revenue, number of transactions, and average transaction value (AVG(Total)) by Branch and by City. Which branch/city performs best in each metric?



