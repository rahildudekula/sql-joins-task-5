-- 🛠️ Step 1: Create customers table
CREATE TABLE customers (
    customer_id INTEGER PRIMARY KEY,
    name TEXT
);

-- 🛠️ Step 2: Create orders table
CREATE TABLE orders (
    order_id INTEGER PRIMARY KEY,
    customer_id INTEGER,
    item TEXT
);

-- 🧩 Step 3: Insert sample data into customers
INSERT INTO customers (customer_id, name) VALUES
(1, 'Alice'),
(2, 'Bob'),
(3, 'Charlie');

-- 🧩 Step 4: Insert sample data into orders
INSERT INTO orders (order_id, customer_id, item) VALUES
(101, 1, 'Pizza'),
(102, 2, 'Burger'),
(103, 4, 'Fries'); -- Note: customer_id 4 does not exist in customers

-- 🔍 INNER JOIN: Only customers with orders
SELECT c.customer_id, c.name, o.item
FROM customers AS c
INNER JOIN orders AS o ON c.customer_id = o.customer_id;

-- 🔍 LEFT JOIN: All customers, with or without orders
SELECT c.customer_id, c.name, o.item
FROM customers AS c
LEFT JOIN orders AS o ON c.customer_id = o.customer_id;

-- 🔍 RIGHT JOIN: All orders, even if customer not found
-- Note: RIGHT JOIN is not supported in SQLite, but is in MySQL
-- If using SQLite, simulate RIGHT JOIN like a LEFT JOIN by reversing tables
SELECT c.customer_id, c.name, o.item
FROM customers AS c
RIGHT JOIN orders AS o ON c.customer_id = o.customer_id;

-- 🔍 FULL OUTER JOIN: Everything from both tables
-- SQLite does not support FULL OUTER JOIN directly
-- Use UNION of LEFT JOIN and RIGHT JOIN
SELECT c.customer_id, c.name, o.item
FROM customers AS c
LEFT JOIN orders AS o ON c.customer_id = o.customer_id

UNION

SELECT c.customer_id, c.name, o.item
FROM customers AS c
RIGHT JOIN orders AS o ON c.customer_id = o.customer_id;
