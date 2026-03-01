# Spark Transformations vs Actions (Layman Guide + Examples + Interview Answers)

## 1) Core Idea (Simple)

In Spark operations are of two types:

**Transformations** → Define what to do (lazy)
**Actions** → Trigger execution (run now)

Think:

* Transformations = plan
* Actions = execute

---

## 2) What is a Transformation?

A **transformation** creates a new dataset from existing one but does NOT execute immediately.

Examples:

* filter
* select
* map
* groupBy
* join

They only build DAG.

---

## 3) Transformation Example

```python
df = spark.read.csv("sales.csv")
df2 = df.filter(df.city == "BLR")
df3 = df2.select("amount")
```

At this stage:

* No data processed
* No job run
* Only plan built

---

## 4) What is an Action?

An **action** asks Spark to produce a result.

Examples:

* show()
* count()
* collect()
* write()
* first()

These trigger execution.

---

## 5) Action Example

```python
df3.show()
```

Now Spark:

* Builds stages
* Allocates executors
* Processes partitions
* Returns result

Execution happens here.

---

## 6) Why Spark Separates Them

Because Spark can:

✔ Optimize whole pipeline
✔ Merge operations
✔ Reduce passes
✔ Avoid unnecessary work

---

## 7) Pipeline Example

Code:

```python
spark.read.csv("sales.csv") \
  .filter("city = 'BLR'") \
  .groupBy("city") \
  .sum("amount") \
  .show()
```

Transformations:

* read
* filter
* groupBy
* sum

Action:

* show

Execution only once at end.

---

## 8) Without Transformation/Action Separation

Each step would run separately:

* read → execute
* filter → execute
* group → execute

Multiple disk passes → slow.

Spark avoids this.

---

## 9) Internal Execution Flow

User code
→ Transformations recorded
→ DAG built
→ Action called
→ DAG optimized
→ Jobs/stages/tasks created
→ Execution

---

## 10) Multiple Actions Behavior

```python
df = spark.read.csv("sales.csv")
df2 = df.filter(df.city == "BLR")

print(df2.count())
print(df2.count())
```

Spark executes twice.

Because:

* Transformations lazy
* No cached result

Use cache():

```python
df2.cache()
df2.count()
df2.count()
```

Now second is fast.

---

## 11) Common Transformations List

* select
* filter
* map
* flatMap
* groupBy
* join
* distinct
* orderBy

---

## 12) Common Actions List

* show
* count
* collect
* take
* first
* write
* save

---

## 13) Key Differences Table

| Feature      | Transformation  | Action       |
| ------------ | --------------- | ------------ |
| Execution    | Lazy            | Immediate    |
| Output       | New dataset     | Result/value |
| Builds DAG   | Yes             | No           |
| Triggers job | No              | Yes          |
| Recomputes   | Yes (if reused) | N/A          |

---

## 14) Real‑World Analogy

Transformations:
Shopping list planning.

Actions:
Going to store and buying.

---

## 15) Interview Questions & Answers

### Q1: What is transformation in Spark?

Lazy operation that defines dataset transformation without executing.

---

### Q2: What is action in Spark?

Operation that triggers execution and returns result.

---

### Q3: When does Spark execute transformations?

Only when an action is called.

---

### Q4: Why multiple actions slow job?

Each action triggers full recomputation unless cached.

---

### Q5: How to avoid recomputation?

Cache or persist dataset.

---

## 16) One‑Line Memory Trick

Transformations plan; actions run.

---

## 17) Key Takeaways

* Transformations are lazy
* Actions trigger execution
* DAG built from transformations
* Multiple actions cause recomputation
* Cache avoids repeated work

---

**End of Notes**
