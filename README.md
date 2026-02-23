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

---

## 🟡 2. Revenue & Product-Level Aggregation

3. What is the total revenue generated overall and broken down by product line/category?

4. What is the total revenue and quantity sold by Product line? Rank the product lines from highest to lowest revenue.

5. Which product line has the highest total quantity sold?

6. Which product line has the highest average unit price?

---

## 🟠 3. Advanced Product Metrics

7. For each Product line, what is the average Unit price and average Quantity purchased? Which product line has the highest average spend per transaction?

---

## 🔵 4. Customer & Gender Analysis

8. What is the distribution of customer types — count and percentage of total sales?

9. How do sales differ by gender?

10. Which gender contributes more to revenue in each product line?

---

## 🟣 5. Time-Based Analysis

11. Extract the month and day of week from the Date column. Which month has the highest total sales? Which day of the week is busiest?

---

## 🔴 6. Branch & City Performance (Advanced KPIs)

12. Calculate total sales revenue, number of transactions, and average transaction value (AVG(Total)) by Branch and by City. Which branch/city performs best in each metric?



