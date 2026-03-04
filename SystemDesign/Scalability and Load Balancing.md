# System Design – Scalability & Load Balancing

## 1. What is Scalability?

In simple terms, scalability means:

Can your system handle growth?

Growth in:

* Users
* Traffic
* Data
* Requests per second

If today your app handles 1,000 users and tomorrow 1 million users, does it still work smoothly?
That is scalability.

---

# 2. Types of Scalability

## 2.1 Vertical Scaling (Scale Up)

Add more power to same machine.

Example:

* Increase RAM from 8GB → 64GB
* Upgrade CPU

Pros:

* Simple
* No architecture change

Cons:

* Has limit
* Expensive
* Single point of failure

Think of it like buying a bigger truck instead of adding more trucks.

---

## 2.2 Horizontal Scaling (Scale Out)

Add more machines instead of upgrading one.

Example:
Instead of 1 server handling 10,000 requests,
Use 10 servers handling 1,000 each.

Pros:

* Highly scalable
* Fault tolerant

Cons:

* More complex
* Needs load balancer

This is what big systems use.

---

# 3. What is Load Balancing?

Load balancing means distributing traffic across multiple servers.

Instead of:
User → One server (overloaded)

We do:
User → Load Balancer → Multiple servers

The load balancer decides which server handles each request.

---

# 4. Why Load Balancing is Important

Without load balancer:

* One server crashes → System down
* Uneven traffic → Slow performance

With load balancer:

* Traffic distributed evenly
* If one server fails → others handle traffic

---

# 5. Load Balancing Algorithms

## 5.1 Round Robin

Requests go in order:
Server1 → Server2 → Server3 → repeat

Simple and common.

---

## 5.2 Least Connections

Request goes to server with least active connections.

Useful when requests take different time.

---

## 5.3 IP Hash

Same user IP always goes to same server.

Useful for session-based systems.

---

# 6. Real-World Tools

Popular load balancers:

* Nginx
* HAProxy
* AWS Elastic Load Balancing

Caching tools for scalability:

* Redis

Message queues for scaling async tasks:

* Apache Kafka

---

# 7. Example 1 – Scaling a Web Application

Problem:
Your website gets 1 million users per day.

Solution:

1. Add Load Balancer
2. Add multiple App Servers
3. Add Database Replicas
4. Add Cache layer

Flow:
User → Load Balancer → App Server → Cache → Database

If data found in cache → fast response
Else → fetch from DB → store in cache

This reduces database load.

---

# 8. Example 2 – E-commerce Sale Traffic Spike

During festival sale:
Traffic increases 10x.

Scaling strategy:

* Auto-scale application servers
* Use CDN for static files
* Use read replicas
* Queue background tasks (emails, invoices)

This prevents system crash.

---

# 9. Handling Database Scalability

## 9.1 Read Replicas

One primary DB
Multiple read replicas

Write → Primary
Read → Replicas

Improves performance.

---

## 9.2 Sharding

Split data across multiple databases.

Example:
Users A–M → DB1
Users N–Z → DB2

Reduces load on single database.

---

# 10. Interview Questions & Answers

## Q1: How do you scale a system?

Answer structure:

* Horizontal scaling
* Load balancer
* Caching
* Database replication
* Async processing

---

## Q2: When do you choose vertical vs horizontal scaling?

Vertical:

* Small system
* Quick fix

Horizontal:

* Large scale system
* High availability required

---

## Q3: How does load balancer improve availability?

If one server fails:
Load balancer removes it from rotation.
Traffic goes to healthy servers.

System stays up.

---

## Q4: What is a single point of failure?

If one component fails and whole system stops.

Example:
Only one database server without replication.

---

# 11. Common Mistakes in Interviews

* Forgetting load balancer
* Ignoring database scaling
* Not discussing failure handling
* Overcomplicating solution

---

# 12. Final Summary

Scalability = Handle growth.
Load Balancing = Distribute traffic.

Good scalable system:

* Horizontally scalable
* Fault tolerant
* Uses caching
* Uses replication
* Avoids single point of failure

In interviews, always:

1. Clarify scale
2. Design simple system first
3. Add scaling step by step
4. Discuss trade-offs

That structured thinking is what interviewers look for.
