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

## A Deeper Dive on ACID Compliance

### 💥 What is ACID Compliance?

ACID stands for:
- Atomicity
- Consistency
- Isolation
- Durability

These are four key properties that ensure reliable transactions in a database. Let’s break each one down with simple definitions and examples.

### 🔍 1. Atomicity – “All or Nothing”

> A transaction is atomic if all parts of it succeed, or none at all. If one part fails, the entire transaction is rolled back.

#### 🔧 Example:
You transfer money from Account A to B:

- Deduct $100 from A ✅
- Add $100 to B ✅

If the system crashes after deducting from A but before adding to B — atomicity ensures both steps are rolled back, so no money is lost.

### 🧮 2. Consistency – “Valid States Only”

> A transaction must move the database from one valid state to another — preserving all rules (constraints, triggers, etc.).

#### 🔧 Example:
You have a constraint: account_balance >= 0.  

A transaction that results in a negative balance must fail, or it would violate consistency.

### ⛓️ 3. Isolation – “No Interference”

> Multiple transactions running at the same time shouldn’t interfere with each other.

#### 🔧 Example:
Two users book the last concert ticket at the same time. Isolation ensures that:

- Only one of the bookings completes. 
- The other waits or fails, avoiding overbooking.

Isolation levels (like Read Committed, Repeatable Read, Serializable) control how much transactions can “see” each other.

### 🔒 4. Durability – “It Sticks”

> Once a transaction is committed, it will persist, even if there’s a system crash.

##### 🔧 Example:
After confirming a payment, the data is saved to disk. Even if the server crashes, the transaction is not lost.

### 🧠 Why is ACID Important?

Because databases often run critical operations, ACID ensures:

- Data integrity (no partial writes, invalid states, etc.)
- Reliability in financial systems, inventory systems, etc.
- Trust from users that their operations are safe and predictable

### ⚠️ Without ACID?

Imagine a banking app:

- Money disappears (atomicity broken)
- Double bookings (isolation broken)
- Dirty data (consistency broken)
- Transactions vanish after a crash (durability broken)
😱 Not ideal.

###  Real-World Examples

System	| ACID?	| Notes
--------| --------| ---------
PostgreSQL	| ✅ Full ACID	| Relational DB with strong guarantees
MySQL (InnoDB)	| ✅	| MyISAM engine is not ACID
MongoDB	| ✅ (since v4.0 for multi-doc)	| Wasn't ACID for multi-doc transactions before
Redis	| 🚫 (by default)	| Can be made durable with AOF, but not full ACID
Cassandra	| 🚫	| Prioritizes availability over consistency (AP in CAP)

### 🧾 TL;DR Summary

Property	| Meaning	| Keyword
------------| --------| ---------
Atomicity	| All-or-nothing	| Rollback
Consistency	| Only valid data	| Constraints
Isolation	| No cross-talk between transactions	| Concurrency
Durability	| It survives crashes	| Persistence