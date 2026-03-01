# Transactions & Isolation Levels (Layman Guide + Examples + Interview Answers)

## 1) What is a Transaction? (Simple idea)

A **transaction** is a group of database actions that should be treated as **one single unit of work**.

👉 Either **all steps succeed**, or **none of them happen**.

Real‑life analogy: Online bank transfer

* Step 1: Deduct money from your account
* Step 2: Add money to receiver account

If step 2 fails, step 1 must be undone.
That full operation = **transaction**.

---

## 2) Why Transactions Matter

Without transactions, data becomes incorrect:

* Money deducted but not received
* Order placed but payment missing
* Seat booked twice

Transactions guarantee **data safety and consistency**.

---

## 3) ACID Properties (Interview must‑know)

Transactions follow **ACID** rules:

### A — Atomicity (All or Nothing)

Either everything happens or nothing happens.

Example:
Transfer ₹500

* Deduct succeeds
* Add fails
  → System rolls back deduction

✔ No partial result allowed

---

### C — Consistency (Valid State)

Data must remain correct before and after transaction.

Example:
Total bank money must stay same

* A loses 500
* B gains 500

✔ No money created/destroyed

---

### I — Isolation (No Interference)

Multiple transactions should not disturb each other.

Example:
Two people booking last seat
Only one must succeed.

---

### D — Durability (Permanent)

Once committed, data stays saved even after crash.

Example:
After payment success, order remains even if system restarts.

---

## 4) What is Isolation Level?

When many users access data simultaneously, problems occur.

Isolation level = **how strictly transactions are separated from each other**.

Think: "How much can others see while I'm working?"

---

## 5) Problems Without Isolation (Concurrency Issues)

### 1) Dirty Read

Reading uncommitted data.

Example:
T1: Updates price = 100 → not committed
T2: Reads 100
T1: Rolls back → price back to 50

T2 saw wrong value → Dirty read

---

### 2) Non‑Repeatable Read

Same query gives different result in same transaction.

Example:
T1 reads salary = 50k
T2 updates salary = 60k and commits
T1 reads again → 60k

Value changed unexpectedly.

---

### 3) Phantom Read

New rows appear during transaction.

Example:
T1: Count employees = 10
T2: Inserts new employee
T1: Count again = 11

New "phantom" row appeared.

---

## 6) SQL Isolation Levels (From weakest → strongest)

### 1) Read Uncommitted (Lowest safety)

Can read uncommitted data.

✔ Fast
❌ Dirty reads possible

Use: Rarely used

---

### 2) Read Committed (Most common default)

Only committed data visible.

✔ No dirty reads
❌ Non‑repeatable reads possible
❌ Phantom reads possible

Use: General apps

---

### 3) Repeatable Read

Rows read once cannot change.

✔ No dirty reads
✔ No non‑repeatable reads
❌ Phantom reads possible (in some DBs)

Use: Financial systems

---

### 4) Serializable (Highest safety)

Transactions behave like executed one‑by‑one.

✔ No dirty reads
✔ No non‑repeatable reads
✔ No phantom reads

❌ Slowest

Use: Critical banking/ledger

---

## 7) Isolation Level Comparison Table

| Isolation Level  | Dirty Read | Non‑Repeatable | Phantom | Speed   |
| ---------------- | ---------- | -------------- | ------- | ------- |
| Read Uncommitted | YES        | YES            | YES     | Fastest |
| Read Committed   | NO         | YES            | YES     | Fast    |
| Repeatable Read  | NO         | NO             | YES*    | Medium  |
| Serializable     | NO         | NO             | NO      | Slow    |

---

## 8) SQL Examples

### Start Transaction

```sql
BEGIN;
```

### Commit

```sql
COMMIT;
```

### Rollback

```sql
ROLLBACK;
```

---

### Set Isolation Level

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

---

## 9) Simple Real‑World Example

Bank transfer ₹1000

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE id = 2;

COMMIT;
```

If error occurs:

```sql
ROLLBACK;
```

---

## 10) How Databases Enforce Isolation

They use:

* Locks (row/table locks)
* MVCC (multi‑version copies)

Goal: Prevent conflicts while allowing concurrency.

---

## 11) Interview Questions & Answers

### Q1: What is a transaction?

A transaction is a group of database operations executed as a single unit that either fully succeeds or fully fails.

---

### Q2: What are ACID properties?

Atomicity, Consistency, Isolation, Durability — rules ensuring reliable transactions.

---

### Q3: Difference: Read Committed vs Repeatable Read?

Read Committed: data can change if reread.
Repeatable Read: same rows stay stable during transaction.

---

### Q4: What is dirty read?

Reading data modified by another transaction that hasn’t committed.

---

### Q5: Highest isolation level?

Serializable.

---

### Q6: Why not always Serializable?

It reduces performance and concurrency due to heavy locking.

---

## 12) When to Use Which Level

Use Read Committed:

* Most applications
* Web systems

Use Repeatable Read:

* Financial data
* Reports

Use Serializable:

* Banking core
* Inventory correctness critical

---

## 13) One‑Line Memory Trick

Transactions = Safe unit of work
Isolation = How separate concurrent work stays

---

## 14) Key Takeaways

* Transaction = all‑or‑nothing database operation
* ACID = safety rules
* Isolation levels control concurrency effects
* Serializable = safest, slowest
* Read Committed = most common

---

**End of Notes**
