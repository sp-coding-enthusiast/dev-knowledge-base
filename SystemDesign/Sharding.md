# System Design – Database Sharding

## 1. What is Database Sharding?

In simple words:
Sharding means splitting a large database into smaller pieces and storing them on different servers.

Instead of:
One big database handling all users

We do:
Multiple smaller databases handling parts of the data.

Think of it like dividing a huge class of 1,000 students into 10 smaller classrooms of 100 students each.

---

# 2. Why Do We Need Sharding?

As data grows:

* Database becomes slow
* Queries take longer
* Writes become bottleneck
* One server cannot handle load

Sharding helps to:

* Distribute load
* Improve performance
* Increase scalability

---

# 3. When Do We Use Sharding?

Use sharding when:

* Data is very large (millions/billions of records)
* Single database cannot handle traffic
* Vertical scaling is not enough

Sharding is usually used in high-scale systems.

---

# 4. Types of Sharding Strategies

## 4.1 Range-Based Sharding

Split data based on ranges.

Example:
Users with ID 1–1,000,000 → DB1
Users with ID 1,000,001–2,000,000 → DB2

Pros:

* Simple to implement

Cons:

* One shard can become overloaded if new users always go to latest range

---

## 4.2 Hash-Based Sharding

Use a hash function on shard key.

Example:
shard = user_id % 4

If result:
0 → DB1
1 → DB2
2 → DB3
3 → DB4

Pros:

* Even distribution

Cons:

* Hard to change number of shards later

---

## 4.3 Directory-Based Sharding

Maintain a lookup table that tells which data is stored in which shard.

Example:
User123 → DB2
User456 → DB4

Pros:

* Flexible

Cons:

* Extra complexity
* Lookup service can become bottleneck

---

# 5. Example – Social Media Application

Problem:
App has 200 million users.
Single database is slow.

Solution:
Shard users based on user_id using hash-based sharding.

Flow:
User login → Hash user_id → Identify shard → Query correct database.

Each shard handles only part of the data.

System becomes scalable.

---

# 6. Example – E-commerce Orders

Orders table growing rapidly.

Option:
Shard by region.

India orders → DB1
US orders → DB2
Europe orders → DB3

Improves performance and reduces cross-region latency.

---

# 7. Challenges in Sharding (Very Important)

## 7.1 Re-Sharding Problem

If you add new shard later,
Data redistribution becomes complex.

---

## 7.2 Cross-Shard Queries

Example:
"Find total orders across all users"

Now system must query all shards and combine results.

This increases complexity.

---

## 7.3 Joins Become Difficult

Joining tables across shards is hard.

That’s why NoSQL systems often used with sharding.

---

## 7.4 Hotspot Problem

If one shard gets too much traffic,
it becomes overloaded.

Example:
All celebrity users stored in one shard.

---

# 8. Sharding vs Replication

Sharding:

* Splits data
* Improves write scalability

Replication:

* Copies same data
* Improves read performance and availability

Large systems use BOTH.

---

# 9. Interview Questions & How to Answer

## Q1: When should you shard a database?

Answer:
When vertical scaling is not enough and database becomes performance bottleneck.

---

## Q2: How do you choose shard key?

Answer:
Shard key should:

* Distribute data evenly
* Avoid hotspots
* Be frequently used in queries

---

## Q3: What are challenges of sharding?

Answer:

* Cross-shard queries
* Rebalancing data
* Increased complexity
* Difficult joins

---

## Q4: Can sharding improve read performance?

Yes, because reads are distributed across multiple databases.
But replication is usually better for read scaling.

---

# 10. Common Mistakes in Interviews

* Saying sharding solves everything
* Forgetting shard key discussion
* Ignoring cross-shard query issues
* Not mentioning re-sharding complexity

---

# 11. Final Summary

Database Sharding = Splitting data across multiple databases to scale horizontally.

Benefits:

* Better scalability
* Improved performance
* Distributed load

Challenges:

* Complexity
* Cross-shard queries
* Rebalancing

In interviews always explain:

1. Why sharding is needed
2. Shard key selection
3. How data is routed
4. Trade-offs and challenges

That clear structured explanation shows strong system design understanding.
