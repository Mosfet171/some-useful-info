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

## ⚡ Indexing

### 🧠 What is Indexing?
Indexing is like a book’s table of contents: it helps the database find data faster without scanning the entire table.

### 🔍 Without an index:
If you query:

```
SELECT * FROM users WHERE email = 'alice@example.com';
```

The database may need to scan every row in the users table to find a match (called a full table scan).

### 🚀 With an index:
It uses a fast lookup structure (often a B-tree or hash) to jump directly to the matching rows — much faster!

### ✅ Benefits:
- Drastically improves read/query speed for large datasets
- Helps in searching, filtering (WHERE), joining, and sorting (ORDER BY)

### ❌ Downsides:
- Slows down writes (INSERT, UPDATE, DELETE) because the index must also be updated
- Takes additional disk space

### 🔧 How to create one:
```
CREATE INDEX idx_users_email ON users(email);
```

You can also use:

- Composite indexes (multiple columns)
- Unique indexes (to prevent duplicates)
- Full-text indexes (for searching large text)

## 🧬 Normalization

### 🧠 What is Normalization?
Normalization is the process of organizing data into tables to reduce redundancy and ensure data integrity.

It means:

- Avoiding duplicate data
- Splitting large tables into related smaller tables
- Using foreign keys to relate data

### 🏗️ Example (Before Normalization):
A students table might look like:

id | name | course1 | course2
---| ---- | ------- | -------
1	| Alice	| Math	| Physics

Problems:

- Redundant structure
- What if a student takes 5 courses?
- Hard to query/filter on course

### 🏗️ After Normalization:
students table:

id	| name
---- | ----
1	| Alice

courses table:

id	| name
----| ----
1	| Math
2	| Physics

student_courses (join table):

student_id	| course_id
--------| -------
1	| 1
1	| 2

Now:

- Flexible & scalable
- No data duplication
- Easy to query

### 🧪 Normal Forms (NF)
These are levels of normalization, each stricter than the last:

Normal | Form	Rule
------ | --------
1NF	| No repeating groups, atomic values (each cell = 1 value)
2NF	| 1NF + no partial dependencies (use IDs, not embedded data)
3NF	| 2NF + no transitive dependencies (no derived or indirect info)

💡 Most real-world databases aim for 3NF, then denormalize slightly if performance needs it.

### 🧠 Summary

Concept	| Indexing	| Normalization
------- | --------  | -----------
Purpose	| Speed up searching & filtering	| Eliminate redundancy, improve structure
Main Benefit	| Faster queries	| Clean, consistent data
Downside	| Slower writes, more disk use	| More complex queries (joins)
Use When	| Query performance matters	| Designing schema for maintainability

