# SQL Execution Plans — Explained in Simple Terms

## What is an Execution Plan?

When you run a SQL query, the database must decide:

* Which table to read first
* Whether to use an index or scan
* How to join tables
* How to filter rows

That step‑by‑step strategy is called the **execution plan**.

👉 Execution plan = how the database chooses to run your query

---

## Real‑life Analogy

Imagine going from home to office.

Possible routes:

* Shortest distance
* Least traffic
* Highway route
* Metro + walk

Google Maps picks the best route.

SQL optimizer does the same.

👉 Query = destination
👉 Execution plan = chosen route

---

## Simple Example Table

**Users**

| id | name    | city      |
| -- | ------- | --------- |
| 1  | Ravi    | Bangalore |
| 2  | Sita    | Delhi     |
| 3  | Arjun   | Mumbai    |
| 4  | Saurabh | Pune      |
| 5  | Meera   | Delhi     |

---

## Query

```sql
SELECT * FROM Users WHERE name = 'Saurabh';
```

Database has two options:

### Plan A — Table Scan

Check every row:

1 → Ravi
2 → Sita
3 → Arjun
4 → Saurabh ✅

Slow for large tables.

---

### Plan B — Index Seek

If index exists on `name`:

```sql
CREATE INDEX idx_users_name ON Users(name);
```

Database jumps directly to row.

Fast.

---

👉 Execution plan chooses **Index Seek** because cheaper.

---

# Why Execution Plans Matter

They explain:

* Why query is slow
* Whether index is used
* Which join is chosen
* Where time is spent

They are the #1 tool for SQL performance tuning.

---

# Common Operations in Execution Plans

## 1. Table Scan

Reads entire table.

Bad for large tables.

Meaning: no usable index.

---

## 2. Index Seek

Direct lookup via index.

Best case.

---

## 3. Index Scan

Reads large part of index.

Better than table scan but not ideal.

---

## 4. Nested Loop Join

For each row in table A, search table B.

Good when one table small.

---

## 5. Hash Join

Build hash table then match rows.

Good for large datasets.

---

## 6. Sort

Database sorts rows for ORDER BY or GROUP BY.

Can be expensive.

---

# Example with Join

Tables:

**Orders**

| order_id | customer_id | amount |

**Customers**

| customer_id | name |

Query:

```sql
SELECT c.name, o.amount
FROM Orders o
JOIN Customers c
ON o.customer_id = c.customer_id;
```

Execution plan decides:

* Which table first
* Join type
* Index usage

If index exists on `customer_id` → fast join.

---

# How Database Chooses Plan

SQL optimizer estimates cost using:

* Table size
* Index presence
* Data distribution
* Statistics

It picks lowest‑cost plan.

👉 Cheapest plan ≠ shortest SQL text
👉 Cheapest = least work

---

# How to View Execution Plan

## SQL Server

```sql
SET SHOWPLAN_ALL ON;
```

or click “Display Estimated Execution Plan”.

---

## MySQL

```sql
EXPLAIN SELECT * FROM Users WHERE name='Saurabh';
```

---

## PostgreSQL

```sql
EXPLAIN ANALYZE SELECT ...
```

---

# Interview Questions & Answers

## Q1: What is a SQL execution plan?

**Answer:**
A SQL execution plan is the step‑by‑step strategy chosen by the database optimizer to execute a query efficiently, including access methods, join types, and operations.

---

## Q2: Why are execution plans important?

**Answer:**

Execution plans help identify:

* Performance bottlenecks
* Missing indexes
* Expensive operations
* Inefficient joins

They are essential for query tuning.

---

## Q3: Difference between Index Seek and Index Scan?

**Answer:**

* Index Seek → direct lookup of specific rows
* Index Scan → reads many index rows sequentially

Seek is faster.

---

## Q4: What causes table scan?

**Answer:**

* No index on filter column
* Low selectivity
* Small table
* Optimizer decision

---

## Q5: What is cost in execution plan?

**Answer:**

Cost is the optimizer’s estimate of resources (CPU, I/O, memory) required to execute an operation. The optimizer selects the lowest‑cost plan.

---

## Q6: How to improve a bad execution plan?

**Answer:**

* Add proper indexes
* Rewrite query
* Update statistics
* Avoid SELECT *
* Filter earlier

---

# Practical Slow vs Fast Example

Slow query:

```sql
SELECT * FROM Orders WHERE customer_name = 'Ravi';
```

No index → table scan.

Add index:

```sql
CREATE INDEX idx_customer_name ON Orders(customer_name);
```

Execution plan changes → index seek.

Query becomes fast.

---

# Key Takeaways

* Execution plan = query route map
* Shows how DB runs query
* Reveals scans, seeks, joins
* Used for performance tuning
* Optimizer picks cheapest plan

---

# One‑Line Interview Summary

👉 "A SQL execution plan is the optimizer’s chosen strategy that defines how a query will access data and perform operations to return results efficiently."
