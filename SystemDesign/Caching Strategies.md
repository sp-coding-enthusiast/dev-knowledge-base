# System Design – Caching Strategies

## 1. What is Caching?

In simple words:
Caching means storing frequently used data in a fast storage so we don’t need to fetch it again and again from a slow database.

Example:
Instead of asking the database for the same product details 1,000 times,
we store it in cache and return it instantly.

Think of cache like keeping frequently used books on your study table instead of going to the library every time.

---

# 2. Why Do We Need Caching?

Without cache:

* Database gets overloaded
* System becomes slow
* High latency

With cache:

* Faster response time
* Reduced database load
* Better scalability

Most large-scale systems heavily depend on caching.

---

# 3. Where Can We Cache?

## 3.1 Client-Side Cache

Stored in browser or mobile app.

Example:
Browser caching images or static files.

---

## 3.2 CDN Cache

Stores static files (images, CSS, JS) closer to users globally.

Useful for high-traffic applications.

---

## 3.3 Server-Side Cache

Stored in memory using tools like Redis or Memcached.

Most common in system design interviews.

---

# 4. Common Caching Strategies

## 4.1 Cache-Aside (Lazy Loading)

Most common strategy.

Flow:

1. Application checks cache.
2. If data found → return it.
3. If not found → fetch from database.
4. Store result in cache.
5. Return to user.

Pros:

* Simple
* Cache only what is needed

Cons:

* First request slower

Example:
User searches product → Not in cache → Fetch from DB → Save in cache → Next user gets fast response.

---

## 4.2 Write-Through Cache

Flow:

1. Application writes data to cache.
2. Cache writes data to database immediately.

Pros:

* Cache always consistent with DB

Cons:

* Write latency increases

Example:
User updates profile → Data written to cache and DB together.

---

## 4.3 Write-Back (Write-Behind)

Flow:

1. Write to cache first.
2. Cache updates DB later (async).

Pros:

* Very fast writes

Cons:

* Risk of data loss if cache crashes

Used when write speed is critical.

---

## 4.4 Read-Through Cache

Application does not talk to DB directly.
Cache itself fetches data from DB on miss.

Application → Cache → (if miss) → DB

Cleaner architecture but more setup required.

---

# 5. Cache Eviction Policies

Cache memory is limited. We must remove old data.

## 5.1 LRU (Least Recently Used)

Removes data that was not used recently.

Most popular policy.

## 5.2 LFU (Least Frequently Used)

Removes data used least number of times.

## 5.3 TTL (Time To Live)

Data expires after fixed time.

Example:
OTP stored for 5 minutes only.

---

# 6. Example – E-commerce Product Page

Problem:
Product page is accessed 100,000 times per hour.

Without cache:
All requests hit database → DB overloaded.

With cache-aside:

1. First request → DB → Store in cache.
2. Next 99,999 requests → Cache only.

Huge performance improvement.

---

# 7. Example – Social Media Feed

User opens app frequently.
Feed data changes often.

Solution:

* Cache recent feed data
* Use TTL to expire quickly
* Combine with async updates

Balance between freshness and performance.

---

# 8. Cache Invalidation (Very Important)

Hardest problem in caching.

Question:
When should cached data be removed or updated?

Methods:

* TTL expiry
* Manual invalidation on update
* Versioning

If not handled properly:
Users see stale (old) data.

---

# 9. Interview Questions & How to Answer

## Q1: Which caching strategy is most common?

Answer:
Cache-aside because it is simple and gives good control.

---

## Q2: How do you handle stale data?

Answer:

* Use TTL
* Invalidate cache on updates
* Use versioning

---

## Q3: Where should we use write-back cache?

Answer:
When write performance is critical and slight delay in DB update is acceptable.

---

## Q4: What are risks of caching?

Answer:

* Stale data
* Cache inconsistency
* Cache crash causing data loss (in write-back)

---

# 10. Common Mistakes in Interviews

* Adding cache without explaining invalidation
* Ignoring consistency problems
* Not discussing eviction policy
* Overcomplicating design

---

# 11. Final Summary

Caching improves:

* Performance
* Scalability
* User experience

Most used strategy in interviews:
Cache-aside + TTL + LRU.

Always explain:

1. Where cache is placed
2. How data is written
3. How data is invalidated
4. Trade-offs

That structured explanation makes you stand out in system design interviews.
