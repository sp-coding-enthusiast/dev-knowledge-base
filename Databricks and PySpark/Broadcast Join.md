# Broadcast Joins in Databricks / PySpark

## 1. What is a Broadcast Join? (Layman Explanation)

Imagine you have two lists:

* A huge list of all customers in a country (millions)
* A small list of VIP customers (100 rows)

You want to match who is VIP.

Instead of sending the huge list everywhere, you simply **give the small VIP list to every worker** and let them check locally.

👉 Sending the small table to all machines = **Broadcast**
👉 Joining locally without moving big data = **Broadcast Join**

---

## 2. Why Broadcast Join is Needed

Normally in Spark joins:

* Both tables are shuffled across cluster
* Data moves over network
* Slow

With broadcast join:

* Small table copied to all executors
* No shuffle of big table
* Much faster

Real-world analogy:

* 1 big warehouse + small price list
* Give price list to every worker
* Workers label items locally
* No need to move warehouse stock

---

## 3. When to Use Broadcast Join

Use broadcast when:

* One table is small (few MBs)
* Other table is huge
* Join key exists

Typical case:

* fact table (big)
* dimension table (small)

---

## 4. Broadcast Join Example in PySpark

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import broadcast

spark = SparkSession.builder.getOrCreate()

orders = [(1,101),(2,102),(3,103),(4,101)]
customers = [(101,"Alice"),(102,"Bob"),(103,"Charlie")]

orders_df = spark.createDataFrame(orders,["order_id","cust_id"])
customers_df = spark.createDataFrame(customers,["cust_id","name"])

result = orders_df.join(broadcast(customers_df),"cust_id")
```

Here:

* customers_df is small
* Broadcast to all executors
* orders_df not shuffled

---

## 5. What Happens Internally

Without broadcast:

* orders shuffled
* customers shuffled
* network heavy

With broadcast:

* customers copied to each executor
* orders stays partitioned
* join happens locally

So Spark avoids shuffle of big table.

---

## 6. How Spark Decides to Broadcast Automatically

Spark auto-broadcasts if table size < threshold.

Default:

```
10 MB
```

Config:

```python
spark.conf.set("spark.sql.autoBroadcastJoinThreshold",10485760)
```

Set -1 to disable auto broadcast.

---

## 7. Broadcast Join vs Normal Join

Normal Join:

* shuffle both tables
* slow

Broadcast Join:

* broadcast small table
* no shuffle of big table
* fast

---

## 8. Performance Impact Example

Scenario:

* orders = 1 billion rows
* customers = 10k rows

Normal join → minutes
Broadcast join → seconds

Because big table never moves.

---

## 9. When NOT to Use Broadcast

Avoid when small table is actually large:

* > 100 MB
* many columns
* memory pressure

Because broadcast copied to every executor memory.

If cluster has 20 executors:

50 MB table → 1 GB total memory usage

---

## 10. Broadcast Join in Databricks SQL

```sql
SELECT /*+ BROADCAST(customers) */
*
FROM orders
JOIN customers
ON orders.cust_id = customers.cust_id
```

Hint forces broadcast.

---

## 11. Best Practices

### 1. Broadcast dimension tables

```python
fact.join(broadcast(dim),"id")
```

---

### 2. Select only needed columns

```python
broadcast(dim.select("id","name"))
```

---

### 3. Filter before broadcast

```python
small = dim.filter("country='India'")
fact.join(broadcast(small),"id")
```

---

### 4. Check execution plan

```python
df.explain()
```

Look for:

```
BroadcastHashJoin
```

---

## 12. Interview Questions & Answers

### Q1: What is broadcast join in Spark?

Broadcast join is a join optimization where the smaller dataset is distributed to all executors so the larger dataset does not need to be shuffled.

---

### Q2: Why is broadcast join faster?

Because it avoids shuffle of large dataset and performs join locally in each executor.

---

### Q3: When should broadcast join be used?

When one table is small enough to fit in executor memory and the other is large.

---

### Q4: How to force broadcast in PySpark?

Using broadcast() function from pyspark.sql.functions.

---

### Q5: How to verify broadcast join?

Check physical plan for BroadcastHashJoin.

---

## 13. Strong Databricks Interview Answer

“In Spark, broadcast join is used when one dataset is significantly smaller than the other. Spark distributes the smaller dataset to all executors, allowing each partition of the large dataset to join locally without shuffle. This avoids network transfer of large data and significantly improves join performance. We typically broadcast dimension tables in fact–dimension joins.”

---

## 14. Quick Summary

Broadcast = send small table everywhere
Avoid shuffle of big table
Best for fact–dimension joins
Check plan → BroadcastHashJoin

---

**End of Notes**
