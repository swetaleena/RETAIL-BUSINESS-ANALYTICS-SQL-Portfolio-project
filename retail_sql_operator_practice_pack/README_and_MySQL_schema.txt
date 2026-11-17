RETAIL BUSINESS ANALYTICS – SQL OPERATOR PRACTICE PACK
Target DB: MySQL 8.0+
All data is fictional and designed for learning.

FILES
- products.csv
- customers.csv
- orders.csv
- order_items.csv
- suppliers.csv
- purchase_orders.csv
- employee_access.csv

RELATIONSHIPS
products.product_id = order_items.product_id
orders.order_id = order_items.order_id
customers.customer_id = orders.customer_id
suppliers.supplier_id = purchase_orders.supplier_id
products.product_id = purchase_orders.product_id

IMPORT
Create a database, then create tables using the schema below. Import each CSV into its matching table using MySQL Workbench's Table Data Import Wizard.
Dates use YYYY-MM-DD. Empty received_date cells represent NULL.

SUGGESTED TABLE DEFINITIONS
CREATE DATABASE retail_operator_lab;
USE retail_operator_lab;

CREATE TABLE products (
 product_id INT PRIMARY KEY, product_name VARCHAR(100), category VARCHAR(50),
 category_id INT, list_price DECIMAL(10,2), cost_price DECIMAL(10,2),
 stock_qty INT, is_active TINYINT
);
CREATE TABLE customers (
 customer_id INT PRIMARY KEY, customer_name VARCHAR(100), city VARCHAR(60),
 state VARCHAR(60), signup_date DATE, customer_type VARCHAR(30)
);
CREATE TABLE orders (
 order_id INT PRIMARY KEY, customer_id INT, order_date DATE,
 order_status VARCHAR(30), payment_method VARCHAR(30), ship_city VARCHAR(60),
 priority_flag INT
);
CREATE TABLE order_items (
 order_item_id INT PRIMARY KEY, order_id INT, product_id INT,
 quantity INT, unit_price DECIMAL(10,2), discount_amount DECIMAL(10,2)
);
CREATE TABLE suppliers (
 supplier_id INT PRIMARY KEY, supplier_name VARCHAR(100), city VARCHAR(60),
 specialty VARCHAR(50)
);
CREATE TABLE purchase_orders (
 purchase_order_id INT PRIMARY KEY, supplier_id INT, product_id INT,
 order_date DATE, received_date DATE NULL, quantity INT,
 unit_cost DECIMAL(10,2), po_status VARCHAR(30)
);
CREATE TABLE employee_access (
 employee_id INT PRIMARY KEY, employee_name VARCHAR(80), department_id INT,
 job_title VARCHAR(60), permission_mask INT
);

NOTE ON IMPORT
For reliable imports, create the tables first, then use Table Data Import Wizard.
If using LOAD DATA LOCAL INFILE, enable local infile in your MySQL client and use
FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS.
Use NULL handling for empty received_date cells if your import method loads them as empty strings.

OPERATOR NOTES
- Arithmetic and comparison operators work directly in MySQL.
- Logical operators ALL, AND, ANY, BETWEEN, EXISTS, IN, LIKE, NOT, OR, SOME are supported.
  SOME is a synonym for ANY.
- MySQL bitwise operators: &, |, ^, ~, <<, >>. The page lists &, |, ^, ~.
- The compound assignment operators shown on the W3Schools page are not MySQL assignment syntax.
  For MySQL, use SET stock_qty = stock_qty + 5 rather than stock_qty += 5.
  Similarly use SET permission_mask = permission_mask & 5 rather than &=.
- Run UPDATE exercises only on a practice copy or inside a transaction; ROLLBACK after practice.