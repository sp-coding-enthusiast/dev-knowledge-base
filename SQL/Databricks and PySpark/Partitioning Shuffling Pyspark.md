# Partitioning & Shuffling in Databricks / PySpark

## 1. What is Partitioning? (Layman Explanation)

Imagine you have a huge book with millions of pages and you ask 10 people to read it quickly. Instead of giving the whole book to one person, you divide the book into 10 parts and give each person one part.

**That division is called partitioning.**

In PySpark, large datasets are split into smaller chunks called **partitions** so multiple machines can process data in parallel.

👉 More partitions = more parallel processing (faster)
👉 Too many partitions = overhead (slower)

---

## 2. Why Partitioning is Important

Without partitioning:

* One machine handles everything → slow

With partitioning:

* Many machines process in parallel → fast

Real‑world analogy:

* Sorting 1 crore exam papers
* 1 teacher → days
* 100 teachers → hours

---

## 3. What is Shuffling? (Layman Explanation)

Shuffling means **moving data between partitions/machines** based on some condition.

Imagine students from different cities sitting randomly in classrooms. Now you want all students from the same city in the same room.

So students move between rooms.

👉 That movement = **shuffle**

In PySpark, shuffle happens when Spark redistributes data across partitions.

---

## 4. When Does Shuffle Happen in PySpark?

Shuffle occurs during operations like:

* groupBy()
* join()
* distinct()
* reduceByKey()
* repartition()

Because Spark must rearrange data based on keys.

---

## 5. Partitioning Example in PySpark

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.getOrCreate()

data = [(1,"A"),(2,"B"),(3,"C"),(4,"D"),(5,"E")]
df = spark.createDataFrame(data, ["id","value"])

print(df.rdd.getNumPartitions())
```

Output may be: 2

Meaning data is split into 2 partitions.

---

## 6. Repartition vs Coalesce

### Repartition

* Increases or decreases partitions
* Causes shuffle

```python
df2 = df.repartition(4)
```

Now data redistributed across 4 partitions.

---

### Coalesce

* Only reduces partitions
* Avoids shuffle (mostly)

```python
df3 = df.coalesce(1)
```

Good when writing small output files.

---

## 7. Shuffle Example (groupBy)

```python
data = [("India",100),("India",200),("US",300),("US",400)]
df = spark.createDataFrame(data,["country","amount"])

result = df.groupBy("country").sum()
```

What Spark does internally:

Before shuffle:
Partition 1 → India, US
Partition 2 → India, US

After shuffle:
Partition A → India, India
Partition B → US, US

Then aggregation happens.

---

## 8. Why Shuffle is Expensive

Shuffle involves:

* Disk I/O
* Network transfer
* Serialization

So it is the **most expensive Spark operation**.

Interview line:
👉 “Shuffle is expensive because it redistributes data across executors over network.”

---

## 9. How to Reduce Shuffle (Best Practices)

### 1. Use partitioning column wisely

```python
df.repartition("country")
```

Now same‑country data stays together.

---

### 2. Use broadcast join

```python
from pyspark.sql.functions import broadcast

big.join(broadcast(small),"id")
```

Avoids shuffle of big table.

---

### 3. Avoid unnecessary repartition

Bad:

```python
df.repartition(1000)
```

---

### 4. Use reduceByKey instead of groupByKey (RDD)

Reduces shuffle size.

---

## 10. Partitioning in Databricks Tables

Databricks also supports table partitioning:

```sql
CREATE TABLE sales
USING DELTA
PARTITIONED BY (country)
```

Data stored as:

```
/country=India/
/country=US/
```

Query becomes faster:

```sql
SELECT * FROM sales WHERE country='India'
```

Only India folder scanned.

---

## 11. Key Interview Questions & Answers

### Q1: What is partitioning in Spark?

Partitioning is splitting large dataset into smaller chunks so they can be processed in parallel across cluster nodes.

---

### Q2: What is shuffle in Spark?

Shuffle is redistribution of data across partitions during operations like join, groupBy, and aggregation.

---

### Q3: Why is shuffle expensive?

Because it involves disk I/O, network transfer, and serialization between executors.

---

### Q4: Difference between repartition and coalesce?

Repartition increases/decreases partitions with shuffle.
Coalesce reduces partitions without full shuffle.

---

### Q5: How to reduce shuffle in Spark?

* Broadcast join
* Proper partitioning
* Avoid unnecessary repartition
* Filter early

---

## 12. Real Databricks Interview Answer (Strong)

“In Spark, data is divided into partitions which enable parallel processing across executors. When transformations like join or groupBy require data with same keys to be colocated, Spark performs shuffle — redistributing data across partitions over network and disk. Since shuffle is costly, we optimize using broadcast joins, proper partitioning columns, and minimizing repartition operations.”

---

## 13. Quick Summary

Partitioning = splitting data for parallelism
Shuffle = moving data between partitions
Shuffle = expensive
Goal = minimize shuffle

---

**End of Notes**
