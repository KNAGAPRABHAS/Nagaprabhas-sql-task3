# Nagaprabhas-sql-task3
---

# Task 3: SQL for Data Analysis

## Objective

The objective of this task is to utilize SQL to extract, manipulate, and analyze structured data from a relational database. The task covers various SQL operations including filtering, sorting, grouping, joining tables, using subqueries, performing aggregations, creating views, and optimizing queries using indexes.

## Tools

- **Database Engines:** MySQL / PostgreSQL / SQLite (choose any)
- **Interface Tools:** MySQL Workbench, pgAdmin, DB Browser for SQLite, or any preferred SQL client

## Dataset

**Dataset Used:** `Ecommerce_SQL_Database`  
You may use any eCommerce dataset with typical tables such as customers, orders, products, payments, and order details.

### Example Schema

1. **customers**
   - `customer_id`, `name`, `email`, `created_at`
2. **orders**
   - `order_id`, `customer_id`, `order_date`, `total_amount`
3. **order_items**
   - `item_id`, `order_id`, `product_id`, `quantity`, `price`
4. **products**
   - `product_id`, `product_name`, `category`, `price`
5. **payments**
   - `payment_id`, `order_id`, `payment_date`, `amount`, `payment_method`

## Deliverables

- A `.sql` file containing all SQL queries written for analysis
- Screenshots of the query outputs from the database environment
- This `README.md` file documenting the work

## Task Breakdown

### 1. Basic Data Retrieval

**Query:** Select all customers who registered after January 1, 2023.

```sql
SELECT * FROM customers
WHERE created_at > '2023-01-01'
ORDER BY created_at DESC;
```

---

### 2. Aggregated Sales per Product

**Query:** Get total revenue generated per product.

```sql
SELECT p.product_name, SUM(oi.quantity * oi.price) AS total_revenue
FROM order_items oi
JOIN products p ON oi.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_revenue DESC;
```

---

### 3. Top 5 Customers by Spending

**Query:** Use aggregation and sorting to find the top 5 customers.

```sql
SELECT c.name, c.email, SUM(o.total_amount) AS total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id
ORDER BY total_spent DESC
LIMIT 5;
```

---

### 4. Monthly Revenue Summary (View)

**Query:** Create a view to summarize revenue by month.

```sql
CREATE VIEW monthly_sales AS
SELECT DATE_FORMAT(order_date, '%Y-%m') AS month, SUM(total_amount) AS revenue
FROM orders
GROUP BY month
ORDER BY month;
```

**Usage:**

```sql
SELECT * FROM monthly_sales;
```

---

### 5. Orders Without Payments

**Query:** Use a LEFT JOIN to identify orders that have not received payments.

```sql
SELECT o.order_id, o.order_date, c.name
FROM orders o
LEFT JOIN payments p ON o.order_id = p.order_id
JOIN customers c ON o.customer_id = c.customer_id
WHERE p.payment_id IS NULL;
```

---

### 6. Query Optimization with Indexing

**Query:** Add an index to the `order_date` column to improve performance.

```sql
CREATE INDEX idx_order_date ON orders(order_date);
```

---

## How to Run

1. Set up the eCommerce database in your preferred SQL environment.
2. Open the `.sql` file containing the queries.
3. Execute each query and capture a screenshot of the output.
4. Save all screenshots and files in an organized folder for submission.

## Outcome

By completing this task, you will:

- Gain hands-on experience in querying relational databases.
- Understand how to use SQL to summarize, filter, and relate data.
- Learn how to write efficient queries using indexes and views.
- Build the foundational skills required for real-world data analysis with SQL.

## Author

Name: *[Your Name]*  
Institution: *[Your College/Organization]*  
Date: *April 2025*

---

