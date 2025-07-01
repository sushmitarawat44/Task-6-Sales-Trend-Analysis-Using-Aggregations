# 📊 Online Sales Trend Analysis

This project explores an **e-commerce sales dataset** and performs a **monthly revenue and order volume analysis** using SQL. 
The analysis reveals business trends over time to support decision-making and growth strategies.

---

## 📁 Dataset Overview

**Table Name:** Online_Sales

| Column Name     | Description                          |
|-----------------|--------------------------------------|
| customer_id     | Unique ID of each customer           |
| order_date      | Date when the order was placed       |
| product_id      | Unique product identifier            |
| category_id     | Product category ID                  |
| category_name   | Product category name                |
| product_name    | Name of the product                  |
| quantity        | Quantity purchased                   |
| amount          | Total order amount ($)               |
| payment_method  | Payment method used                  |
| city            | Customer's city                      |
| review_score    | Product review score (1 to 5)        |
| gender          | Gender of the customer               |
| age             | Age of the customer                  |

---

## 🎯 Task 6: Sales Trend Analysis Using Aggregations

### 📌 Objective
Analyze **monthly revenue** and **order volume** trends using SQL.

### 🛠️ Tools
- SQLite (via SQLiteStudio)
- SQL (Standard Syntax)

---

## 🧠 Query Logic

``sql
--- Monthly revenue and order volume trend
SELECT 
    strftime('%Y', order_date) AS year,
    strftime('%m', order_date) AS month,
    SUM(amount) AS total_revenue,
    COUNT(DISTINCT order_date || '-' || customer_id) AS order_volume
FROM 
    Online_Sales
GROUP BY 
    year, month
ORDER BY 
    year, month
LIMIT 10;

Dataset : https://www.kaggle.com/datasets/ertugrulesol/online-retail-data/data
