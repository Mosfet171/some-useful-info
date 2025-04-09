# Databases

## 🗃️ What is a Database?
A database is an organized collection of data that can be easily accessed, managed, and updated. It's where applications store info like users, products, messages, etc.

There are two main types of databases:
1. Relational Databases (SQL)
* Data is stored in tables (rows and columns)
* You use SQL (Structured Query Language) to query and manipulate data
* Examples: MySQL, PostgreSQL, SQLite, Microsoft SQL Server
2. Non-Relational Databases (NoSQL)
* Data can be stored in various flexible formats: JSON, key-value pairs, documents, graphs, etc.
* Examples: MongoDB, Redis, Cassandra, Firebase

## 🧠 SQL vs NoSQL – Quick Visual
Feature	| SQL (MySQL/PostgreSQL) | 	NoSQL (MongoDB, etc.)
------- | ---------------------  | --------------------
Structure	| Tables & rows	| Documents, key-value, etc.
Schema	| Fixed (strict schema)	| Flexible schema
Query language	| SQL	| Varies (MongoDB uses JSON-like queries)
Relationships	| Strong (joins, foreign keys)	| Weak or manual
ACID compliance	| Strong	| Often weaker (eventual consistency)
Best for	| Complex queries, reporting	| High scalability, unstructured data


## 🐬 MySQL

### 🔍 What it is:
* A popular open-source relational database developed in the 1990s.
* Widely used in web apps (e.g., WordPress, LAMP stack).

### ✅ Pros:
* Fast for read-heavy workloads
* Easy to learn and manage
* Huge community and support
* Great for transactional systems

### ❌ Cons:
* Limited support for advanced features like window functions (now better in recent versions)
* Not as standards-compliant as PostgreSQL

## 🐘 PostgreSQL

### 🔍 What it is:
* An advanced open-source relational database known for being feature-rich and standards-compliant.

### ✅ Pros:
* More powerful than MySQL for complex queries
* Supports custom data types, JSON, full-text search, geospatial data (PostGIS)
* ACID-compliant, strong support for concurrency and reliability

### ❌ Cons:
* Slightly more complex to set up and tune
* Historically slower than MySQL in read-heavy scenarios (but it's improved)

## 🍃 MongoDB (NoSQL Example)

### 🔍 What it is:
* A document-based NoSQL database
* Stores data as BSON (binary JSON)

### ✅ Pros:
* Schema-less — easy to change data structure
* Scales horizontally well (sharding)
* Great for handling unstructured or semi-structured data

### ❌ Cons:
* No strong JOIN support — not ideal for complex relationships
* Eventual consistency (unless you configure for strict rules)
* Less mature tooling compared to SQL systems

## 🧪 ACID vs BASE
Term |	Description
---- | ------
ACID (SQL)	| Atomicity, Consistency, Isolation, Durability — ensures reliable transactions
BASE (NoSQL)	| Basically Available, Soft state, Eventually consistent — prioritizes availability & scalability

## ⚖️ Which one should you use?
Scenario |	Best Choice
------- | ---------
Web apps with structured data |	MySQL or PostgreSQL
Data analytics, geospatial, JSON mix |	PostgreSQL
Fast reads, simple schema |	MySQL
Massive scale, flexible data |	MongoDB or another NoSQL
Real-time apps, caching	| Redis (NoSQL - key-value)