# Deadlocks (Layman Guide + Examples + Interview Answers)

## 1) What is a Deadlock? (Simple idea)

A **deadlock** happens when two or more transactions are **waiting for each other forever**, and none of them can proceed.

👉 Each transaction holds a resource the other needs.
👉 Both are stuck.

Real‑life analogy: Two cars in a narrow lane

* Car A blocks B
* Car B blocks A
* Neither can move → Deadlock

---

## 2) Database Deadlock Example (Step‑by‑Step)

Two bank transactions:

Transaction T1:

* Locks Account A
* Wants Account B

Transaction T2:

* Locks Account B
* Wants Account A

Now:

* T1 waits for B (held by T2)
* T2 waits for A (held by T1)

👉 Both waiting forever → Deadlock

---

## 3) SQL Deadlock Example

Initial data:

* Account A
* Account B

### Transaction 1

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1; -- locks A
-- waiting to update B
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
```

### Transaction 2

```sql
BEGIN;
UPDATE accounts SET balance = balance - 50 WHERE id = 2; -- locks B
-- waiting to update A
UPDATE accounts SET balance = balance + 50 WHERE id = 1;
```

Now:

* T1 holds A, needs B
* T2 holds B, needs A

Deadlock occurs.

---

## 4) Why Deadlocks Matter

Without handling deadlocks:

* System freezes
* Transactions never finish
* Users wait forever
* Data updates fail

So databases must detect and resolve them.

---

## 5) How Databases Handle Deadlocks

When deadlock detected:
👉 Database **kills one transaction** (rollback)
👉 Other continues

Killed transaction = **deadlock victim**

Example:

* T1 rolled back
* T2 completes

---

## 6) Conditions Required for Deadlock (4 Rules)

Deadlock happens only if ALL 4 occur:

### 1) Mutual Exclusion

Resource cannot be shared.
(Only one lock allowed)

### 2) Hold and Wait

Transaction holds one lock while waiting for another.

### 3) No Preemption

Locks cannot be forcibly taken.

### 4) Circular Wait

T1 waits for T2, T2 waits for T1.

👉 Break any one → No deadlock

---

## 7) Deadlock vs Blocking (Important Interview Difference)

**Blocking:**
One waits, other finishes → OK

Example:
T1 locks row
T2 waits
T1 commits
T2 continues

✔ Temporary wait

**Deadlock:**
Both wait forever

✔ Circular dependency
✔ Needs DB intervention

---

## 8) How to Prevent Deadlocks (Best Practices)

### 1) Access tables in same order

Always lock A then B (never reverse)

✔ Most effective rule

---

### 2) Keep transactions short

Finish quickly → fewer conflicts

---

### 3) Avoid user interaction inside transaction

Don’t wait for input while holding locks

---

### 4) Use proper indexes

Fewer rows locked → less chance

---

### 5) Lower isolation level (if safe)

Serializable → more locks → more deadlocks

---

## 9) How to Detect Deadlocks (Concept)

Database builds **wait‑for graph**:

T1 → waiting for T2
T2 → waiting for T1

Cycle found → deadlock

---

## 10) Real‑World Examples

### Banking

Transfer A→B and B→A simultaneously

---

### E‑commerce

Order updates inventory + payment
Another updates payment + inventory

---

### Ticket booking

Two users locking seats in reverse order

---

## 11) Interview Questions & Answers

### Q1: What is a deadlock?

A situation where two or more transactions wait indefinitely for each other’s locked resources.

---

### Q2: How does DB resolve deadlock?

By aborting (rolling back) one transaction — the deadlock victim.

---

### Q3: Difference between deadlock and blocking?

Blocking is temporary waiting; deadlock is circular permanent waiting.

---

### Q4: How to prevent deadlocks?

Access resources in same order and keep transactions short.

---

### Q5: Which isolation level increases deadlocks?

Serializable (due to heavy locking).

---

## 12) One‑Line Memory Trick

Deadlock = circular waiting on locks

---

## 13) Key Takeaways

* Deadlock = transactions stuck waiting on each other
* Caused by circular lock dependency
* DB detects and kills one transaction
* Prevention: consistent lock order + short transactions

---

**End of Notes**
