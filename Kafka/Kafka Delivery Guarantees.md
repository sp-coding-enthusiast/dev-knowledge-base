# Kafka Delivery Guarantees (Layman Explanation)

Kafka delivery guarantees define how reliably messages move from producer to consumer.

Kafka provides three guarantees:

- At most once
- At least once
- Exactly once

---

# At Most Once

Message delivered zero or one time.

Possible loss  
No duplicates  

Occurs when offsets are committed before processing.

Used for logs and non-critical data.

---

# At Least Once

Message delivered one or more times.

No loss  
Possible duplicates  

Occurs when offset committed after processing.

Most common Kafka mode.

---

# Exactly Once

Message delivered exactly once.

No loss  
No duplicates  

Achieved using:

- Idempotent producer
- Kafka transactions
- Atomic offset + output commit

Used for payments and financial systems.

---

# Why Duplicates Happen

Consumer processes message but crashes before committing offset.

Kafka resends message → duplicate.

---

# Idempotency

Idempotent processing means same message processed multiple times produces same result.

Required for exactly-once processing.

---

# Comparison

At most once:
- Possible loss
- No duplicate

At least once:
- No loss
- Possible duplicate

Exactly once:
- No loss
- No duplicate

---

# Interview Questions

## What are Kafka delivery guarantees?
At most once, at least once, exactly once.

## Default Kafka guarantee?
At least once.

## How duplicates occur?
Crash before offset commit.

## How exactly once achieved?
Transactions and idempotent producer.

## Safest guarantee?
Exactly once.

## Most used?
At least once.