# Spark Lazy Evaluation (Layman Guide + Examples + Interview Answers)

## 1) What is Lazy Evaluation? (Simple idea)

**Lazy evaluation** means Spark does NOT execute operations immediately when you write them.

👉 Spark waits
👉 Builds a plan
👉 Executes only when result needed

Think: Making a to‑do list first, working later.

---

## 2) Why Spark Uses Lazy Evaluation

If Spark executed every step instantly:

* Many unnecessary computations
* More disk I/O
* Slower performance

Instead Spark:
✔ Optimizes whole pipeline
✔ Removes redundant steps
✔ Combines operations

---

## 3) Simple Example

```python
df = spark.read.csv("sales.csv")
df2 = df.filter(df.city == "BLR")
df3 = df2.select("amount")
```

At this point:
👉 Nothing executed
👉 No data read yet

Execution happens only at:

```python
df3.show()
```

---

## 4) Transformations vs Actions (Core Idea)

### Transformations → Lazy

* filter
* select
* groupBy
* join

They just build plan.

---

### Actions → Trigger Execution

* show
* count
* collect
* write

They need result → Spark runs pipeline.

---

## 5) How Lazy Evaluation Works Internally

When you write transformations:

Spark builds DAG:

Read → Filter → Select → Aggregate

No execution yet.

When action called:

Spark optimizes DAG
→ splits into stages
→ executes tasks

---

## 6) Optimization Benefits

Lazy evaluation allows:

✔ Predicate pushdown
✔ Projection pruning
✔ Stage fusion
✔ Shuffle reduction

Example:
If only one column needed,
Spark reads only that column.

---

## 7) Real‑World Example

Task: Total sales in Bangalore

Code:

```python
spark.read.parquet("sales") \
  .filter("city = 'BLR'") \
  .groupBy("city") \
  .sum("amount") \
  .show()
```

Lazy steps:

* read planned
* filter planned
* group planned

Execution only at show().

---

## 8) Without Lazy Evaluation (Hypothetical)

Each step runs separately:

* read full data
* write temp
* read again
* filter
* write temp

Very slow.

Lazy evaluation avoids this.

---

## 9) Lazy Evaluation + DAG Example

Pipeline:

Read → Filter → Select → Count

Spark merges into single optimized stage.

Instead of 3 passes → 1 pass.

---

## 10) Caching Interaction

Normally lazy.

But if cached:

```python
df.cache()
df.count()
```

Now materialized in memory.

Future actions reuse data.

---

## 11) When Lazy Evaluation Happens Multiple Times

```python
df = spark.read.csv("sales.csv")
df2 = df.filter(df.city == "BLR")

print(df2.count())
print(df2.count())
```

Spark executes twice (unless cached).

Because no stored result yet.

---

## 12) Key Advantages

* Global optimization
* Fewer passes on data
* Reduced I/O
* Better parallelism
* Efficient execution plan

---

## 13) Interview Questions & Answers

### Q1: What is lazy evaluation in Spark?

Spark delays execution of transformations until an action is called.

---

### Q2: Why Spark uses lazy evaluation?

To optimize the full execution plan and reduce unnecessary computation.

---

### Q3: Difference between transformation and action?

Transformations build DAG; actions trigger execution.

---

### Q4: Does transformation execute immediately?

No — only when action runs.

---

### Q5: How to avoid recomputation?

Use cache or persist.

---

## 14) One‑Line Memory Trick

Transformations are lazy; actions execute.

---

## 15) Key Takeaways

* Spark waits before executing
* Builds DAG first
* Runs only at action
* Enables optimization
* Improves performance

---

**End of Notes**
