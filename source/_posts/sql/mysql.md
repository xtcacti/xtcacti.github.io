---
title: mysql
date: 2021-04-21 10:38:25
tags: mysql
---

## what I will learn?

- Retrieve insert update delete
- Tables Relationships Joins Subquires RegularExpressions
- SELECT WHERE AND OR NOT IN BETWEEN LIKE REGEXP NULL

## what

1. DataBase

- is a collection of data stored in a format that can be easily be accessed

2. DBMS

- DataBase Management System

3. Relational

- Customers - Orders - Products
- Structured Query Language
  - e.g.
  ```
  SELECT *
  FROM prosucts
  WHERE category = 'food'
  ORDER BY price
  ```
- RDBMS
  - MySQL
  - SQL Server
  - Oracle

4. Not Relational - NoSQL

- NoSQL systems don't underdstand SQL

5. SQL & SEQUEL

- SQL:
  - Structured
  - Query
  - Languauge
- SEQUEL:
  - Structured
  - English
  - Query
  - Languauge

## Install MySQL and Workbench

## Connect MySQL

`mysql -u root -p`

## DataBase Operations

### Create DataBase

`CREATE DATABASE db1`

### Drop DataBase

`DROP DATABASE db1`

### Choose DataBase to use

`USE db1`

## DataBase Table Operations

- DataBase Table Record Relationship row column

```
USE sql_store;

SELECT *
FROM customers
-- WHERE customer_id = 1
ORDER BY first_name
```

### Create Table

```
CREATE TABLE `order_statuses` (
  `order_status_id` tinyint(4) NOT NULL,
  `name` varchar(50) NOT NULL,
  PRIMARY KEY (`order_status_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
INSERT INTO `order_statuses` VALUES (1,'Processed');
INSERT INTO `order_statuses` VALUES (2,'Shipped');
INSERT INTO `order_statuses` VALUES (3,'Delivered');
```

### Drop Table

`DROP TABLE order_statuses`

### SELECT Clause

- `SELECT`

```
SELECT
    last_name,
    first_name,
    points,
    (points+10)*100 AS 'discount factor'
FROM customers
ORDER BY points
```

- `DISTINCT`：remove duplicate

```
SELECT DISTINCT state
FROM customers
```

- `WHERE`: give a condition

```
SELECT *
FROM customers
-- WHERE points > 3000
WHERE state <> 'VA'
-- > >= < <= = != <>
```

- `AND` `OR` `NOT`

```
SELECT *
FROM customers
-- WHERE birth_date >='1900-01-01' OR (points > 1000 AND state = 'VA')
WHERE NOT (birth_date < '1900-01-01' AND (points > 1000 AND state = 'VA'))
```

- `IN` `NOT IN`

```
SELECT *
FROM customers
-- WHERE state = 'VA' OR state = 'FL' OR state = 'GA'
WHERE state IN ('VA','FL','GA')
-- WHERE state NOT IN ('VA','FL','GA')
```

- `BETWEEN...AND...`

```
SELECT *
FROM products
-- WHERE quantity_in_stock >=50 AND quantity_in_stock <= 100
WHERE quantity_in_stock BETWEEN 50 AND 100
```

- `LIKE` - `%` `_` `REGEXP`
  - `%`:pattern any number of chars
  - `_`:pattern single char

```
SELECT *
FROM products
WHERE name LIKE 'P%'
-- WHERE name LIKE '%p%'
-- WHERE name LIKE '%y'
-- WHERE name LIKE '_y'
-- WHERE name REGEXP '^P'
-- WHERE name REGEXP 'e$'
-- WHERE name REGEXP 'e$|^P'
-- WHERE name REGEXP 'P[ogh]'
```

- `IS NULL` `IS NOT NULL`

```
SELECT *
FROM orders
WHERE shipped_date IS NULL
```

- `ORDER BY`

```
SELECT *
FROM order_items
ORDER BY quantity,unit_price DESC
```

```
SELECT quantity,unit_price
FROM order_items
ORDER BY 1,2 DESC
```

- `LIMIT`

```
SELECT *
FROM products
ORDER BY quantity_in_stock DESC
LIMIT 0,3
-- will get first 3 record which stock most
```

-`INNER JOIN`:`JOIN...ON...` 读取匹配的数据

```
-- with one Database
SELECT order_id,o.customer_id,first_name,last_name
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
```

```
-- with two Database
USE sql_store;

SELECT order_id,oi.product_id,p.unit_price,p.name
FROM order_items oi
JOIN sql_inventory.products p
	ON oi.product_id = p.product_id

```

```
-- with self table
USE sql_hr;

SELECT *
FROM employees e
JOIN employees m
	ON e.reports_to = m.employee_id
```

```
-- join multiple table
USE sql_store;

SELECT
	o.order_id,
    o.order_date,
    c.first_name,
    c.last_name,
    os.order_status_id,
    os.name
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
JOIN order_statuses os
	ON o.status - os.order_status_id
- Outer Join:`LEFT JOIN...ON...`
```

- Compound Join Conditions

```
USE sql_store;

SELECT *
FROM order_items oi
JOIN order_item_notes oin
	ON oi.order_id = oin.order_Id
    AND oi.product_id = oin.product_Id
```

- Implpicit Join Syntax

```
SELECT *
FROM orders o,customers c
WHERE o.customer_id = c.customer_id
```

- `OUTER JOIN`
  - `INNER JOIN`: 左连接 就是会读取左表的所有数据
  - `OUTER JOIN`：右连接，就是会读取右表的所有数据

```
USE sql_store;

SELECT
	c.customer_id,
    c.first_name,
    o.order_id
FROM orders o
RIGHT JOIN customers c
	ON c.customer_id = o.customer_id
```

- `CROSS JOIN`

```
SELECT *
FROM orders o,customers c
-- o的每一条记录都会和c的每一条记录合并
```

```
SELECT *
FROM orders o
CROSS JOIN customers c
```

- `USING` Clause

```
USE sql_store;

SELECT
	c.customer_id,
    c.first_name,
    o.order_id
FROM orders o
RIGHT JOIN customers c
	-- ON c.customer_id = o.customer_id
    USING (customer_id)
```

```
SELECT *
FROM order_items oi
JOIN order_item_notes oin
    -- ON oi.order_id = oin.order_id AND oi.product_id = oin.product_id
    USING(order_id,product_id)
```

- `NATURAL JOIN`:去掉

```
USE sql_store;

SELECT
	c.customer_id,
    c.first_name,
    o.order_id
FROM orders o
NATURAL JOIN customers c
```

- `UNION`:连接两个以上的 Select 结果组合到一个结果集合中，默认会删除重复记录，且结果列数必须一样，否则报错

```
USE sql_store;

SELECT
	order_id,
    order_date,
    'Archived' AS status
FROM orders
WHERE order_date < '2019-01-01'

UNION
-- UNION ALL 会保留重复项

SELECT
	order_id,
    order_date,
    'Active' AS status
FROM orders
WHERE order_date >= '2019-01-01'
```

### `INSERT INTO...VALUES...`

```
INSERT INTO customers(
    first_name,
    last_name,
    birth_date,
    address,
    ciry,
    state
)
VALUES (
    'Join',
    'Smith',
    '1990-01-01'
    'address',
    'city',
    'CA'
    )
```

- Inserting Multiple Rows

```
USE sql_store;

INSERT INTO shippers (name)
VALUES ('Shipper1'),
('Shipper2'),
('Shihpper3')
```

- Insert Hierarchical Rows

### Column Attributes

1. VARCHAR
2. INT
3. DATE

### Create a copy to a table

```
USE sql_store;

CREATE TABLE orders_archived AS
SELECT * FROM orders
-- 主键消失了 得额外加主键
```

### Update a single row

```
UPDATE invoices
SET payment_total = 10,
	payment_date='2019-03-11'
WHERE invoice_id = 3
```

### Update multiple rows

```
UPDATE invoices
SET payment_total = 10,
	payment_date='2019-03-11'
WHERE invoice_id IN (3,4)
```

### Using Subqueries in Updates

```
UPDATE invoices
SET payment_total = 10,
	payment_date='2019-03-11'
WHERE client_id =
		(SELECT client_id
        FROM clients
        WHERE name='Vinte'
        )
```

### DELETE ROWS

```
DELETE FROM invoices
WHERE invoice_id=1
```

### Restore the database

archived your sql file and reimport your sql file

## MySQL Function

### IFNULL

- `SELECT IFNULL(var1,var2)` : 如果 var1 不为空，返回 var1，否则返回 var2

```
SELECT
    (SELECT DISTINCT
            Salary
        FROM
            Employee
        ORDER BY Salary DESC
        LIMIT 1 OFFSET 1) AS SecondHighestSalary;
```

## Reference

https://programmingwithmosh.com/wp-content/uploads/2019/03/SQL-Cheat-Sheet.pdf

> 声明：本站所有内容仅供个人学习娱乐笔记所用，如涉侵权，请联系删除

## Master of SQL

### Database design

### Security

### Writing complex quires

### Transactions

### Events
