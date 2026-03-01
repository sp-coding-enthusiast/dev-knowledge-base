# Normalization vs Denormalization (Layman Guide + Examples + Interview Answers)

## 1) What is Normalization? (Simple idea)

**Normalization** means organizing data into separate tables to **remove duplication** and keep data clean.

👉 Store each fact only once.
👉 Link tables using IDs.

Real‑life analogy: Contact list
Instead of repeating city name in every contact,
you store city once and reference it.

---

## 2) Example of Unnormalized Data (Bad Design)

| OrderID | CustomerName | City      | Product | Price |
| ------- | ------------ | --------- | ------- | ----- |
| 1       | Ravi         | Bangalore | Laptop  | 70000 |
| 2       | Ravi         | Bangalore | Mouse   | 500   |

Problems:

* Customer & city repeated
* Update city → many rows
* Risk of inconsistency

---

## 3) Normalized Design (Good Design)

### Customers Table

| CustomerID | Name | City      |
| ---------- | ---- | --------- |
| 101        | Ravi | Bangalore |

### Orders Table

| OrderID | CustomerID | Product | Price |
| ------- | ---------- | ------- | ----- |
| 1       | 101        | Laptop  | 70000 |
| 2       | 101        | Mouse   | 500   |

Now:
✔ No duplication
✔ Easy updates
✔ Consistent data

---

## 4) Benefits of Normalization

* Removes redundancy
* Prevents anomalies
* Saves storage
* Improves data integrity

---

## 5) What is Denormalization? (Simple idea)

**Denormalization** means intentionally **adding duplication back** to improve read speed.

👉 Combine tables
👉 Store repeated data
👉 Faster queries

---

## 6) Denormalized Example

| OrderID | CustomerName | City      | Product | Price |
| ------- | ------------ | --------- | ------- | ----- |
| 1       | Ravi         | Bangalore | Laptop  | 70000 |
| 2       | Ravi         | Bangalore | Mouse   | 500   |

Why allowed here?
Because analytics/reporting reads faster without joins.

---

## 7) Why Denormalization is Used

Joins are expensive on large data.

Normalized query needs:

* Join Customers + Orders

Denormalized query:

* Single table read

✔ Faster reads
❌ More storage
❌ Update complexity

---

## 8) Normalization vs Denormalization (Key Differences)

| Feature          | Normalization  | Denormalization  |
| ---------------- | -------------- | ---------------- |
| Data duplication | Minimal        | Increased        |
| Storage          | Less           | More             |
| Read speed       | Slower (joins) | Faster           |
| Write speed      | Faster         | Slower           |
| Data consistency | High           | Lower            |
| Use case         | OLTP           | OLAP / analytics |

---

## 9) When to Use Normalization

Use in transactional systems:

* Banking
* Orders
* Inventory
* User data

Goal: correctness

---

## 10) When to Use Denormalization

Use in read‑heavy systems:

* Reporting
* Dashboards
* Data warehouse
* Analytics queries

Goal: speed

---

## 11) SQL Example (Normalized Query)

```sql
SELECT o.OrderID, c.Name, c.City, o.Product, o.Price
FROM Orders o
JOIN Customers c ON o.CustomerID = c.CustomerID;
```

---

## 12) SQL Example (Denormalized Query)

```sql
SELECT OrderID, CustomerName, City, Product, Price
FROM OrdersReport;
```

No joins needed → faster.

---

## 13) Interview Questions & Answers

### Q1: What is normalization?

Organizing data into related tables to remove redundancy and improve integrity.

---

### Q2: What is denormalization?

Adding redundant data intentionally to improve read performance.

---

### Q3: Why normalization is important?

Prevents update anomalies and ensures consistency.

---

### Q4: Why denormalization is used?

To reduce joins and speed up read queries.

---

### Q5: Which is better?

Neither — depends on workload.
OLTP → normalized
OLAP → denormalized

---

## 14) Real‑World Analogy

Normalized:
Library catalog
Book info stored once

Denormalized:
Excel report with repeated book info
Easy to read quickly

---

## 15) One‑Line Memory Trick

Normalization = remove duplicates
Denormalization = add duplicates for speed

---

## 16) Key Takeaways

* Normalization improves integrity
* Denormalization improves performance
* OLTP uses normalized design
* Analytics uses denormalized design
* Trade‑off: consistency vs speed

---

**End of Notes**
