# 📊  Task 6: Sales Trend Analysis Using Aggregations

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

## 🎯 Online Sales Trend Analysis

### 📌 Objective
Analyze **monthly revenue** and **order volume** trends using SQL.

### 🛠️ Tools
- SQLite (via SQLiteStudio)
- SQL (Standard Syntax)

---

## 🛠️ Data Preprocessing (Manual Edits in Excel)
Before importing the dataset into SQLite for query analysis, the following manual data cleaning steps were performed using Microsoft Excel:

Filling Missing Values

Review Score: Calculated the average review score (≈ 4) and filled all missing values in the review_score column using Excel's filter and replace functionality.

Gender: Replaced blank entries in the gender column with "Unknown" to ensure consistency and avoid null-related issues in analysis.

Formatting Date Values

Order Date: The original order_date column was in dd/mm/yyyy format, which SQLite does not parse natively. Used Text to Columns with / as a delimiter to split the date.
Reordered the columns into the format yyyy-mm-dd. Used Format Cells → Custom → yyyy-mm-dd to apply the new format.
Recombined and saved the file before importing into SQLite.

---

##🧠 Query Logic

`Extract month from order date`
SELECT 
  strftime('%m', order_date) AS month
FROM Online_Sales
LIMIT 10;

`Group by Year and Month`
SELECT 
  strftime('%Y', order_date) AS year,
  strftime('%m', order_date) AS month,
  COUNT(*) AS total_orders
FROM Online_Sales
GROUP BY year, month
LIMIT 10;

`Use SUM() for Monthly Revenue`
SELECT 
  strftime('%Y', order_date) AS year,
  strftime('%m', order_date) AS month,
  SUM(amount) AS total_revenue
FROM Online_Sales
GROUP BY year, month
ORDER BY year, month
LIMIT 10;

`Use COUNT(DISTINCT order_id) for Order Volume`
SELECT 
  strftime('%Y', order_date) AS year,
  strftime('%m', order_date) AS month,
  COUNT(DISTINCT customer_id || '-' || order_date) AS order_volume
FROM Online_Sales
GROUP BY year, month
ORDER BY year, month
LIMIT 10;

`Use ORDER BY to Sort Results (Descending)`
SELECT 
  strftime('%Y', order_date) AS year,
  strftime('%m', order_date) AS month,
  SUM(amount) AS revenue
FROM Online_Sales
GROUP BY year, month
ORDER BY year DESC, month DESC
LIMIT 10;

`Limit to a Specific Year (e.g., 2022)`
SELECT 
  strftime('%Y', order_date) AS year,
  strftime('%m', order_date) AS month,
  SUM(amount) AS total_revenue,
  COUNT(DISTINCT customer_id || '-' || order_date) AS order_volume
FROM Online_Sales
WHERE strftime('%Y', order_date) = '2024'
GROUP BY year, month
ORDER BY month;

`Monthly revenue and order volume trend`

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
LIMIT 10;`

Dataset : https://www.kaggle.com/datasets/ertugrulesol/online-retail-data/data
