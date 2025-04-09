# Relational Databases Operations

## 🧠 What is a Relational Database?

A Relational Database stores data in tables. Each table represents a relation (like a spreadsheet), with:
* Rows = records
* Columns = fields (attributes)

You can connect tables using relationships (typically via foreign keys).

## 🧰 Core SQL Operations (CRUD)

Operation | 	SQL Keyword	| Example
-------   |    ----------   | --------
Create	| INSERT	| INSERT INTO users VALUES (...)
Read	| SELECT	| SELECT * FROM users
Update	| UPDATE	| UPDATE users SET name = 'Bob'
Delete	| DELETE	| DELETE FROM users WHERE id=1

## 🔗 What is a JOIN?
A JOIN connects data from two or more tables based on a related column (usually a foreign key).

Let’s say you have:

`users` table:
id	|  name
--- | ---- 
1	| Alice
2	| Bob

`orders` table:
id	| user_id	| item
--- | --------- | -----
1	| 1	| Laptop
2	| 2	| Headphones
3	| 1	| Keyboard

## 🧩 Types of Joins
1. INNER JOIN
* Returns matching rows only from both tables.

	```
	SELECT users.name, orders.item
	FROM users
	INNER JOIN orders ON users.id = orders.user_id;
	``` 

	Result:
	name  |	item
	----- | -----
	Alice |	Laptop
	Bob |	Headphones
	Alice |	Keyboard

2. LEFT JOIN (or LEFT OUTER JOIN)
* Returns all rows from the left table, plus matching rows from the right table (or NULLs).

	```
	SELECT users.name, orders.item
	FROM users
	LEFT JOIN orders ON users.id = orders.user_id;
	``` 

	Result: Same as INNER JOIN plus any user without orders (would show NULL for item).

3. RIGHT JOIN
	* Like LEFT JOIN, but the opposite: all rows from the right table, and matched ones from the left.

4. FULL OUTER JOIN
	* Returns all rows from both tables, with NULLs where there’s no match.
	* Not supported in MySQL by default (PostgreSQL supports it).

5. CROSS JOIN
Returns a cartesian product — every row from Table A matched with every row from Table B.

## 🔍 Other Handy SQL Operations

Operation | 	Example
-------   | ----------
GROUP BY | 	GROUP BY category
ORDER BY | 	ORDER BY created_at DESC
LIMIT | 	LIMIT 10
DISTINCT | 	SELECT DISTINCT country
WHERE | 	WHERE age > 18
HAVING	 | Like WHERE, but used with GROUP BY

## 🧪 Aggregation Functions

Function |	Description
------- | -----------
COUNT() |	Number of rows
SUM() |	Total of a column
AVG() |	Average value
MIN() |	Smallest value
MAX() |	Largest value

## ⚡ Sample Complex Query

```
SELECT u.name, COUNT(o.id) AS order_count
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.name
ORDER BY order_count DESC;
``` 

This gets each user's name and how many orders they’ve made, sorted from most to least.