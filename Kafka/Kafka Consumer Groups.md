# Kafka Consumer Groups (Layman Explanation)

## What is a Consumer Group

A consumer group is a set of consumers that work together to read a Kafka topic.

Kafka ensures each partition is read by only one consumer within a group.

---

# Why Consumer Groups Exist

They provide:

- Load balancing
- Parallel processing
- Scalability
- Fault tolerance

Without groups, all consumers would read duplicate data.

---

# Partition Assignment Rule

Within a consumer group:

One partition → one consumer

Example:

Partitions: 3  
Consumers: 3  

C1 → P0  
C2 → P1  
C3 → P2  

---

# Consumers Less Than Partitions

Consumers read multiple partitions.

Partitions: 3  
Consumers: 2  

C1 → P0 + P1  
C2 → P2  

---

# Consumers More Than Partitions

Extra consumers remain idle.

Partitions: 2  
Consumers: 3  

C1 → P0  
C2 → P1  
C3 → idle  

---

# Multiple Consumer Groups

Different systems can read same topic independently.

Topic: orders  

Groups:
- payment-service
- analytics
- inventory

Each group receives all messages.

---

# Offset in Consumer Groups

Offsets are tracked per:

- partition
- consumer group

So different groups have different progress.

---

# Rebalance

When consumers join or leave a group, Kafka reassigns partitions.

This process is called rebalance.

---

# Key Points

- Consumer group = team of consumers
- Partition read by one consumer per group
- Multiple groups read same topic
- Offsets tracked per group
- Rebalance on join/leave
- Max parallelism = partitions

---

# Interview Questions

## What is consumer group?
Group of consumers sharing partitions of a topic.

## Can multiple consumers read same partition?
Not in same group.

## Why consumer groups needed?
Parallel processing and load balancing.

## What is rebalance?
Partition reassignment among consumers.

## What determines parallelism?
Number of partitions.

## Do groups get same data?
Yes, independently.

## How offsets stored?
Per group and partition.