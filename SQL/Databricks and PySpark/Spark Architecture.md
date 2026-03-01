# Spark Architecture (Layman Guide + Examples + Interview Answers)

## 1) What is Spark? (Simple idea)

**Apache Spark** is a distributed data processing engine that can process large data across many machines in parallel.

👉 Big data split across cluster
👉 Tasks executed simultaneously
👉 Results combined

Think: Many workers processing parts of a big job.

---

## 2) Why Spark Architecture Exists

Single machine cannot handle:

* TB/PB data
* Fast analytics
* Parallel computation

Spark distributes work across cluster.

---

## 3) Core Components of Spark Architecture

Spark has 3 main parts:

1. Driver
2. Cluster Manager
3. Executors

---

## 4) Driver (Brain of Spark)

The **Driver** is the main program that controls everything.

Responsibilities:

* Creates Spark session
* Builds execution plan
* Splits job into tasks
* Sends tasks to executors
* Collects results

Think: Project manager.

---

## 5) Cluster Manager (Resource Manager)

The **Cluster Manager** allocates resources (CPU, memory) across machines.

Examples:

* Standalone
* YARN
* Kubernetes

Think: HR allocating workers.

---

## 6) Executors (Workers)

Executors run tasks on data partitions.

Each executor:

* Runs tasks
* Stores data in memory
* Returns results to driver

Think: Workers doing actual work.

---

## 7) How Spark Processes Data (Step‑by‑Step)

Example: Count sales by city

Step 1: Driver reads code

Step 2: Driver builds DAG (plan)

Step 3: Data split into partitions

Step 4: Tasks sent to executors

Step 5: Executors process partitions in parallel

Step 6: Results merged

---

## 8) What is a DAG? (Directed Acyclic Graph)

Spark converts operations into execution graph.

Example operations:

* read
* filter
* groupBy
* sum

Graph shows dependencies.

Why DAG?
✔ Optimization
✔ Parallel planning
✔ Fault recovery

---

## 9) Partitioning (Key Concept)

Big dataset split into pieces.

Example:
1 TB data
→ 100 partitions
→ 100 tasks
→ parallel execution

More partitions = more parallelism.

---

## 10) Lazy Evaluation

Spark does not execute immediately.

It builds plan first.
Execution only when action called.

Example:

```python
df = spark.read.csv("sales.csv")
df2 = df.filter(df.city == "BLR")
```

No execution yet.

Execution happens at:

```python
df2.count()
```

---

## 11) Transformations vs Actions

Transformations (lazy):

* filter
* select
* groupBy

Actions (trigger execution):

* count
* collect
* show
* write

---

## 12) In‑Memory Processing (Why Spark is Fast)

Traditional systems write to disk each step.

Spark keeps data in memory between steps.

✔ Faster iterative processing
✔ Faster ML/analytics

---

## 13) Fault Tolerance (Recovery)

If executor fails:

Spark recomputes lost partition using DAG lineage.

No full restart needed.

---

## 14) Spark Job Hierarchy

Application
→ Job
→ Stage
→ Task

Example:
count() call → job
shuffle boundary → stage
partition work → task

---

## 15) Real‑World Example

Task: Total sales per city from 1TB data

Driver:

* Plans aggregation

Cluster Manager:

* Allocates 50 executors

Executors:

* Each processes partitions
* Computes partial sums

Driver:

* Merges results

---

## 16) Spark Architecture Diagram (Mental Model)

Driver
↓
Cluster Manager
↓
Executors (many)
↓
Data partitions

---

## 17) Interview Questions & Answers

### Q1: What are core Spark components?

Driver, Cluster Manager, Executors.

---

### Q2: What is DAG in Spark?

Execution plan graph of transformations showing dependencies.

---

### Q3: What is lazy evaluation?

Spark delays execution until an action is called.

---

### Q4: What is partition?

A chunk of distributed dataset processed in parallel.

---

### Q5: Why Spark is faster than Hadoop?

In‑memory processing and DAG optimization.

---

## 18) One‑Line Memory Trick

Driver plans, executors run, cluster allocates.

---

## 19) Key Takeaways

* Spark is distributed engine
* Driver controls execution
* Executors process partitions
* DAG enables optimization
* Lazy evaluation improves efficiency
* In‑memory makes Spark fast

---

**End of Notes**
