# Batch vs Streaming Pipelines in Databricks / PySpark (Layman + Examples + Interview)

## 1. What is a Data Pipeline? (Layman Explanation)

A data pipeline is a system that moves and processes data from source to destination.

Example:
App → Processing → Database → Dashboard

---

## 2. Batch Pipeline (Layman Explanation)

Batch means processing data in chunks at intervals.

Example:

* Bank calculates interest at midnight
* Daily sales report
* Payroll processing

So:

Batch = process stored data periodically.

---

## 3. Streaming Pipeline (Layman Explanation)

Streaming means processing data continuously as it arrives.

Example:

* Fraud detection during payment
* Live website analytics
* Real-time alerts

So:

Streaming = process data instantly.

---

## 4. Simple Analogy

Batch:
Collect all letters → deliver once daily

Streaming:
Deliver each letter immediately

---

## 5. Batch Pipeline Example (Databricks)

Daily ETL job:

```python
df = spark.read.format("csv").load("/mnt/sales/2025-01-01")

result = df.groupBy("country").sum("amount")

result.write.format("delta").save("/mnt/delta/daily_sales")
```

Runs once per day.

---

## 6. Streaming Pipeline Example (Databricks)

Continuous ingestion:

```python
stream_df = spark.readStream \
    .format("json") \
    .schema(schema) \
    .load("/mnt/stream/sales")

agg = stream_df.groupBy("country").sum("amount")

agg.writeStream \
    .format("delta") \
    .outputMode("update") \
    .option("checkpointLocation","/mnt/chk") \
    .start("/mnt/delta/live_sales")
```

Runs continuously.

---

## 7. Key Differences

Batch:

* Finite data
* Scheduled
* Higher latency
* Simple

Streaming:

* Infinite data
* Continuous
* Low latency
* Complex

---

## 8. When to Use Batch

* Historical reports
* Backfills
* Large transformations
* Periodic ETL
* Data warehouse loads

---

## 9. When to Use Streaming

* Real-time analytics
* Alerts
* Monitoring
* IoT data
* Fraud detection

---

## 10. Batch vs Streaming Architecture

Batch:
Files → Spark Batch → Delta Table

Streaming:
Kafka/Files → Spark Streaming → Delta Table

---

## 11. Unified Pipelines in Databricks

Databricks supports both.

Example:

Bronze: streaming ingest
Silver: streaming clean
Gold: batch aggregates

So streaming + batch together.

---

## 12. Latency Comparison

Batch:
Minutes → Hours → Days

Streaming:
Seconds → Sub-seconds

---

## 13. Cost Comparison

Batch:
Cheaper (runs occasionally)

Streaming:
Costly (always running)

---

## 14. Fault Tolerance

Batch:
Restart job

Streaming:
Checkpoint + exactly-once

---

## 15. Interview Questions & Answers

### Q1: Difference between batch and streaming pipelines?

Batch pipelines process finite stored data at scheduled intervals, while streaming pipelines process continuously arriving data in near real time.

---

### Q2: When would you choose streaming over batch?

When low latency processing or real-time insights are required, such as fraud detection or monitoring systems.

---

### Q3: Can batch and streaming coexist?

Yes, modern lakehouse architectures combine streaming ingestion with batch aggregation layers.

---

### Q4: Is Spark batch and streaming separate engines?

No, Structured Streaming uses the same Spark engine and APIs as batch processing.

---

### Q5: Example Databricks pipeline design?

Bronze streaming ingestion → Silver streaming transforms → Gold batch aggregates.

---

## 16. Strong Databricks Interview Answer

“Batch pipelines process large volumes of stored data at scheduled intervals, while streaming pipelines process continuously arriving data with low latency. In Databricks lakehouse architecture, both are unified using Spark, where Structured Streaming handles real-time ingestion and transformations, and batch jobs compute periodic aggregates for analytics layers.”

---

## 17. Quick Summary

Batch = periodic data processing
Streaming = real-time processing
Batch = simple & cheap
Streaming = fast & continuous
Databricks = unified pipelines

---

**End of Notes**
