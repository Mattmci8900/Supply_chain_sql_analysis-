# Supply Chain Analysis — SQL Project

## Project Overview
This project analyses the DataCo Smart Supply Chain dataset using PostgreSQL. The dataset contains approximately 180,000 orders and covers customer sales, product categories, delivery performance, shipping methods, and regional profitability across global markets.

The goal was to extract meaningful business insights from raw supply chain data using SQL — identifying trends in customer spending, delivery performance, and profitability that could inform real business decisions.

---

## Dataset
- **Source:** [DataCo Smart Supply Chain Dataset — Kaggle](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis)
- **Size:** ~180,000 rows, 53 columns
- **Tool used:** PostgreSQL via pgAdmin

---

## Business Questions & Queries

### 1. Which customers have the highest total spend?
Identified the top 10 customers by total sales value to highlight the most valuable accounts.

```sql
SELECT customer_id, ROUND(SUM(sales_per_customer), 2) AS total_customer_spend
FROM orders
GROUP BY customer_id
ORDER BY total_customer_spend DESC
LIMIT 10;
```

**Finding:** [Customer 791 had the highest total spend with a total of $9436.61]

---

### 2. Which product categories generate the most revenue?
Ranked the top 5 product categories by total order value.

```sql
SELECT category_name, ROUND(SUM(order_item_total), 2) AS total_revenue
FROM orders
GROUP BY category_name
ORDER BY total_revenue DESC
LIMIT 5;
```

**Finding:** [The top 5 product categories are Fishing, Cleats, Camping, Cardio equipment and Women's Apparel. With fishing being the top product category with a total revenue of $622,693,529 which was $224,407,879 more than the second highest category revenue.]

---

### 3. How are orders distributed across delivery status categories?
Counted the number of orders falling into each delivery status to understand overall delivery performance.

```sql
SELECT delivery_status, COUNT(*) AS number_of_orders
FROM orders
GROUP BY delivery_status
ORDER BY number_of_orders DESC;
```

**Finding:** [From these findings late deliveries have the largest total of 98977 number of orders, meaning that the most common type of delivery is a late delivery followed second by advance shipping.]

---

### 4. Which shipping mode has the highest number of late deliveries?
Filtered for high-risk late deliveries and grouped by shipping mode to identify the worst performing method.

```sql
SELECT shipping_mode, COUNT(late_delivery_risk) AS late_deliveries
FROM orders
WHERE late_delivery_risk = 1
GROUP BY shipping_mode
ORDER BY late_deliveries DESC;
```

**Finding:** [Linking back to the previous question with late deliveries being the most common type of delivery category, the worst performing shipping class of these delivers is Standard class with 41023 late deliveries, with second class having 26987 late deliveries and the best performing class being same day delivery with only 4454 late shipments.]

---

### 5. Which market regions generate the most profit?
Calculated both total profit and average profit per order by region to compare overall performance and efficiency.

```sql
SELECT order_region,
       ROUND(SUM(order_profit_per_order), 2) AS total_profit,
       ROUND(AVG(order_profit_per_order), 2) AS avg_profit_per_order
FROM orders
GROUP BY order_region
ORDER BY total_profit DESC;
```

**Finding:** [Western Europe had the highest total profit per order region with 625,446.08 and an average profit per order of 23.07. Central Asia has the lowest total profit at 13,045.28 and an average profit per order of 23.59, this is a difference in profit of 612,400.80 between the best performing region and the worst.]

---

### 6. Which product categories have high discounts but low profit ratios?
Identified categories where heavy discounting appears to be eroding profit margins — a key insight for pricing strategy.

```sql
SELECT category_name,
       ROUND(AVG(order_item_discount_rate), 3) AS avg_discount_rate,
       ROUND(AVG(order_item_profit_ratio), 3) AS avg_profit_ratio
FROM orders
GROUP BY category_name
ORDER BY avg_discount_rate DESC;
```

**Finding:** [AS seen on TV has the highest discount rate of all the categories with an average discount rate of 0.109 per order, which eats into the average profit per order as this category has the lowest profit margin of all the categories with an average profit of 0.065. Comparing this to the lowest discount rate category being Golf bags & carts with and average discount of 0.093 and an average profit of 0.191.]

---

## Key Insights
- [Late deliveries were the most common delivery outcome, with Standard Class shipping being the worst performer at 41,023 late shipments.]
- [Western Europe was the most profitable region overall, while AS Seen on TV showed the most concerning discount-to-profit relationship across all categories.]

---

## Skills Demonstrated
- Aggregation functions: `SUM`, `COUNT`, `AVG`
- Grouping and sorting: `GROUP BY`, `ORDER BY`
- Filtering: `WHERE`
- Rounding monetary values: `ROUND`
- Aliasing: `AS`
- Limiting results: `LIMIT`

---

## About Me
Aspiring data analyst with 2+ years of experience in logistics and supply chain operations, currently transitioning into data analytics. Building a portfolio in SQL with Python and data visualisation to follow.

[LinkedIn](https://www.linkedin.com/in/matthew-mcintytre-168405268/)
