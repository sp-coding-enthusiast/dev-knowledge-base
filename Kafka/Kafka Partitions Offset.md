# Kafka Partitions & Offsets (Layman Explanation)

## What is Kafka
Apache Kafka is a distributed streaming platform that moves data from producers to consumers.

---

# What is a Partition

A partition is a section of a Kafka topic that stores messages in order.

Topic = collection of partitions  
Partition = ordered log of messages  

Example:

Partition 0:
- Order A
- Order B

Partition 1:
- Order C
- Order D

---

# Why Partitions Exist

Partitions enable:

- Parallel processing
- Scalability
- High throughput
- Distributed consumption

---

# What is an Offset

Offset is the position of a message inside a partition.

Example:

Offset 0 → Order A  
Offset 1 → Order B  
Offset 2 → Order C  

Offsets start from 0 and increase sequentially.

Offsets are unique only within a partition.

---

# Consumer and Offset

Consumer tracks last processed offset.

If last offset = 5  
Next read starts from offset 6

This allows resume after crash without data loss.

---

# Ordering in Kafka

Ordering is guaranteed only within a partition.

Partition 0: A → B → C  
Partition 1: D → E → F  

Global order is not guaranteed.

---

# Partition Selection

Kafka assigns partition using:

- Key hash
- Round-robin
- Custom partitioner

Same key always goes to same partition.

---

# Example

Topic: orders  
Partitions: 3  

Partition 0:
- offset 0 → Order A
- offset 1 → Order B

Partition 1:
- offset 0 → Order C
- offset 1 → Order D

Partition 2:
- offset 0 → Order E

Consumers read partitions in parallel.

---

# Interview Questions

## What is a Kafka partition?
Subset of topic storing ordered messages enabling parallel processing.

## What is offset?
Sequential message ID within partition.

## Are offsets unique across topic?
No. Only within partition.

## Does Kafka guarantee ordering?
Yes, within partition only.

## How consumer resumes?
Using stored offset.

## Can multiple consumers read same partition?
Not in same consumer group.

## Why partitions needed?
Scalability and parallel processing.

## How partition chosen?
Key hash or round-robin.