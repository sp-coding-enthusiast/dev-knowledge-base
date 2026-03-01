# Wide vs Narrow Transformations in PySpark

## 1. Simple (Layman) Explanation

Imagine you and your friends are sorting books.

### Narrow Transformation

Each person works only on the books already in front of them. No one
needs to exchange books with others.

👉 Work stays local.\
👉 Fast.\
👉 No reshuffling.

------------------------------------------------------------------------

### Wide Transformation

Now imagine you must group books by author. Some books need to move from
one person to another.

👉 Books must be reshuffled.\
👉 Data moves across the room.\
👉 Slower because of movement.

In Spark, this movement is called **Shuffle**.

------------------------------------------------------------------------

## 2. Technical Definition

### Narrow Transformation

A transformation where each output partition depends on only one input
partition.

✔ No shuffle\
✔ Faster\
✔ Better performance

Examples: - map() - filter() - flatMap() - union()

------------------------------------------------------------------------

### Wide Transformation

A transformation where output partitions depend on multiple input
partitions.

✔ Shuffle required\
✔ Network + disk I/O\
✔ Slower compared to narrow

Examples: - groupBy() - reduceByKey() - join() - distinct() -
repartition()

------------------------------------------------------------------------

## 3. Example with Code

### Narrow Transformation Example

``` python
rdd = sc.parallelize([1,2,3,4,5])
result = rdd.map(lambda x: x * 2)
```

Here: - Each partition processes its own data. - No data moves between
partitions.

------------------------------------------------------------------------

### Wide Transformation Example

``` python
rdd = sc.parallelize([("A",1),("B",2),("A",3)])
result = rdd.reduceByKey(lambda x,y: x+y)
```

Here: - Spark must bring all "A" values together. - Data is shuffled
across partitions.

------------------------------------------------------------------------

## 4. Key Differences Table

  Feature         Narrow            Wide
  --------------- ----------------- -------------------
  Data Movement   No                Yes (Shuffle)
  Performance     Faster            Slower
  Network Usage   Low               High
  Example         map(), filter()   groupBy(), join()

------------------------------------------------------------------------

## 5. Why Interviewers Ask This

They want to check if you understand:

-   Spark performance tuning
-   Shuffle impact
-   How to optimize pipelines
-   Why some jobs run slow

------------------------------------------------------------------------

## 6. Important Interview Questions & Answers

### Q1: What is the main difference between wide and narrow transformations?

Answer:\
Narrow transformations do not require shuffle because each output
partition depends on a single input partition.\
Wide transformations require shuffle since output partitions depend on
multiple input partitions.

------------------------------------------------------------------------

### Q2: Why are wide transformations slower?

Answer:\
Because they involve shuffle, which includes network transfer, disk I/O,
and sorting.

------------------------------------------------------------------------

### Q3: How can you optimize wide transformations?

Answer: - Reduce shuffle operations - Use reduceByKey instead of
groupByKey - Use proper partitioning - Use broadcast joins when possible

------------------------------------------------------------------------

## 7. Real Interview Tip

If you say: "Wide transformations cause shuffle which increases network
I/O and impacts performance"

You immediately signal strong Spark understanding.

------------------------------------------------------------------------

## 8. Final Memory Trick

Narrow = No movement\
Wide = World tour (data travels)

If data travels → it is wide.
