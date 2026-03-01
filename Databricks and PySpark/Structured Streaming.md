# Structured Streaming in Databricks / PySpark (Layman + Examples + Interview)

## 1. What is Structured Streaming? (Layman Explanation)

Imagine you work in a bank and transactions keep happening every second.

Instead of waiting till end of day to process all transactions, you process them **continuously as they arrive**.

👉 Processing data continuously = **Streaming**
👉 Using Spark tables/DataFrames style = **Structured Streaming**

So:

Structured Streaming = Processing live incoming data using Spark DataFrame APIs.

---

## 2. Batch vs Streaming (Simple Difference)

Batch processing:

* Data already stored
* Process once

Example: yesterday sales report

Streaming processing:

* Data arriving continuously
* Process in real time

Example: live fraud detection

---

## 3. Real-World Examples

* Credit card transactions
* IoT sensor data
* Website clickstream
* Stock prices
* Logs monitoring

All arrive continuously → streaming needed.

---

## 4. Key Idea of Structured Streaming

Spark treats streaming data as **unbounded table** (infinite rows).

You write normal SQL/DataFrame queries.

Spark runs them continuously.

---

## 5. Simple Streaming Example (File Stream)

Read new files as they arrive:

```python
stream_df = spark.readStream \
    .format("json") \
    .schema(schema) \
    .load("/mnt/stream/input")
```

Spark watches folder and processes new files automatically.

---

## 6. Write Stream Output

```python
query = stream_df.writeStream \
    .format("delta") \
    .outputMode("append") \
    .option("checkpointLocation","/mnt/chk") \
    .start("/mnt/output")
```

Now data flows continuously.

---

## 7. Streaming Aggregation Example

Count events per country:

```python
result = stream_df.groupBy("country").count()
```

Spark keeps updating counts as data arrives.

---

## 8. What is Checkpointing?

Streaming must remember progress.

Checkpoint stores:

* processed offsets
* state
* progress

So if job restarts → no data loss.

---

## 9. Output Modes

Append:

* Only new rows

Update:

* Changed rows

Complete:

* Full result each trigger

Example:

```python
.outputMode("append")
```

---

## 10. Triggers (When to Process)

Default: micro-batch (~few seconds)

```python
.trigger(processingTime="10 seconds")
```

Or once:

```python
.trigger(once=True)
```

---

## 11. Watermark (Handling Late Data)

Sometimes data arrives late.

Watermark defines delay tolerance.

```python
stream_df.withWatermark("event_time","10 minutes")
```

Spark waits 10 minutes for late events.

---

## 12. Streaming Join Example

```python
stream_df.join(static_df,"id")
```

Or stream–stream join:

```python
s1.join(s2,"id")
```

Used in event correlation.

---

## 13. Structured Streaming with Delta

Delta is best sink/source.

```python
spark.readStream.format("delta").load(path)
```

```python
.writeStream.format("delta")
```

Supports:

* exactly-once
* schema
* recovery

---

## 14. Streaming Architecture (Simple)

Source → Spark Streaming → Sink

Examples:

Kafka → Spark → Delta
Files → Spark → Table
IoT → Spark → Dashboard

---

## 15. When to Use Structured Streaming

* Real-time analytics
* Monitoring pipelines
* Event processing
* CDC ingestion
* Fraud detection

---

## 16. Interview Questions & Answers

### Q1: What is Structured Streaming?

Structured Streaming is a scalable streaming engine in Spark that processes live data using DataFrame and SQL APIs.

---

### Q2: Difference between batch and streaming?

Batch processes finite stored data, while streaming processes continuously arriving data in near real time.

---

### Q3: What is checkpoint in streaming?

Checkpoint stores processing state and offsets to ensure fault tolerance and exactly-once processing.

---

### Q4: What is watermark?

Watermark defines how long Spark waits for late-arriving data before closing aggregation windows.

---

### Q5: What is micro-batch?

Spark processes streaming data in small batches at regular intervals instead of record-by-record.

---

## 17. Strong Databricks Interview Answer

“Structured Streaming is Spark’s real-time data processing engine that treats streaming data as an unbounded table and allows developers to use DataFrame and SQL operations on continuously arriving data. It processes data in micro-batches with fault tolerance via checkpointing and supports exactly-once semantics, making it suitable for real-time analytics and event-driven pipelines.”

---

## 18. Quick Summary

Streaming = continuous data
Structured = DataFrame API
Micro-batch execution
Checkpoint = recovery
Watermark = late data handling
Delta = best sink

---

**End of Notes**
