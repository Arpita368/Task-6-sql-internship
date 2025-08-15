# Task 6: Subqueries and Nested Queries

## Objective
Use subqueries in SELECT, WHERE, and FROM to implement advanced query logic.

## Tools
MySQL Workbench / DB Browser for SQLite

## Tables
1. Customers (customer_id, name, phone, city, age)
2. Orders (order_id, customer_id, product, price)

## Sample Data
Customers:
(1, 'Ravi Sharma','9745834678', 'Mumbai', 21)
(2, 'Priya Verma','8345587878', 'Delhi', 32)
(3, 'Amit Kumar','9793258778', 'Pune', 25)
(4, 'Neha Singh','9432885346', 'Chennai', 40)
(5, 'Anjali Mehta','9874563210','Mumbai', 30)
(6, 'Rohit Desai','9123456789','Mumbai', 26)
(7, 'Karan Gupta','9988776655','Delhi', 40)
(8, 'Simran Kaur','8877665544','Delhi', 28)

Orders:
(101, 1, 'Laptop', 55000.00)
(102, 1, 'Keyboard', 1500.00)
(103, 2, 'Smartphone', 18000.00)
(104, 3, 'Tablet', 12000.00)

## Queries

--------------------------------
1. Scalar Subquery - Total spending per customer
SELECT name,
       (SELECT SUM(price)
        FROM Orders
        WHERE Customers.customer_id = Orders.customer_id) AS Total_Spending
FROM Customers;
--------------------------------

2. Subquery with IN - Customers who bought products > 20000
SELECT name, phone, city
FROM Customers
WHERE customer_id IN (
    SELECT customer_id
    FROM Orders
    WHERE price > 20000
);
--------------------------------

3. Subquery with EXISTS - Customers who placed at least one order
SELECT customer_id, name
FROM Customers C
WHERE EXISTS (
    SELECT *
    FROM Orders O
    WHERE C.customer_id = O.customer_id
);
--------------------------------

4. Correlated Subquery - Customers older than city average age
SELECT c1.customer_id, c1.name, c1.city, c1.age
FROM Customers c1
WHERE c1.age > (
    SELECT AVG(c2.age)
    FROM Customers c2
    WHERE c1.city = c2.city
);
--------------------------------

5. Subquery in FROM - Customers with avg order price > 20000
SELECT sub.customer_id, sub.avg_price
FROM (
    SELECT customer_id, AVG(price) AS avg_price
    FROM Orders
    GROUP BY customer_id
) AS sub
WHERE sub.avg_price > 20000;

## Outcome
- Learned scalar, correlated, and derived table subqueries
- Practiced IN and EXISTS conditions
- Enhanced ability to write nested SQL logic

## Author
Created by Arpita Jitendra Sonparote
