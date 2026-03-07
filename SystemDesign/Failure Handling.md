# Failure Handling in System Design (Simple Guide) 🛠️

## 1. What is Failure Handling?

In any software system, **failures are inevitable**.

Servers crash, networks fail, databases become slow, and services may stop responding.

**Failure handling** means designing systems so that they can:

- Detect failures
- Recover from failures
- Continue working even when some components fail

### Simple Definition

> Failure handling is the ability of a system to **detect, manage, and recover from errors or failures without crashing the entire system**.

---

# 2. Simple Real-Life Example

### Restaurant Example 🍽️

Imagine you order food at a restaurant.

Normal process:

Customer → Waiter → Kitchen → Food served


But what if:

- The chef is unavailable?
- One ingredient is missing?

Good restaurants **handle failures** by:

- Assigning another chef
- Suggesting alternative dishes
- Informing the customer

They **do not shut down the entire restaurant**.

Software systems should behave the same way.

---

# 3. Types of Failures in Distributed Systems

### 1️⃣ Hardware Failure

Physical machines may fail.

Examples:

- Server crash
- Disk failure
- Power outage

---

### 2️⃣ Network Failure

Communication between services may fail.

Examples:

- Packet loss
- High latency
- Network outage

---

### 3️⃣ Application Failure

Bugs in the code may cause failures.

Examples:

- Null pointer exception
- Memory leak
- Infinite loop

---

### 4️⃣ Dependency Failure

A service depends on another service.

If the dependency fails, the system may break.

Example:
Checkout Service → Payment Service


If payment service fails, checkout fails.

---

# 4. Goals of Failure Handling

Systems should be designed to:

- **Be resilient**
- **Recover quickly**
- **Avoid cascading failures**

Good systems follow the rule:

> Failure should be **isolated**, not **spread across the system**.

---

# 5. Common Failure Handling Techniques

## 1️⃣ Retry Mechanism

If a request fails, the system tries again.

Example:
Service A → Service B


If Service B fails once:
Retry after 1 second
Retry after 2 seconds
Retry after 4 seconds


This is called **exponential backoff**.

Example pseudocode:
retry_count = 3
wait_time = 1s


---

## 2️⃣ Circuit Breaker Pattern

Prevents repeated calls to a failing service.

Example:
Service A → Service B


If B keeps failing:

The circuit breaker **stops sending requests temporarily**.

States:

| State | Meaning |
|---|---|
Closed | Requests allowed |
Open | Requests blocked |
Half-open | Testing recovery |

Benefits:

- Prevents overload
- Protects system stability

---

## 3️⃣ Timeouts

Requests should not wait forever.

Example:
API call timeout = 2 seconds


If response not received within time:

Request fails and fallback happens.

---

## 4️⃣ Fallback Mechanism

Provide **alternative response when failure occurs**.

Example:

E-commerce product recommendation fails.

Fallback:
Show popular products


Instead of showing an error.

---

## 5️⃣ Replication

Store data across multiple servers.

Example:
Primary Database
Replica 1
Replica 2


If primary fails → replica takes over.

---

## 6️⃣ Load Balancing

Traffic is distributed across multiple servers.

Example:

User requests
↓
Load Balancer
↓
Server A
Server B
Server C


If one server fails, others handle traffic.

---

## 7️⃣ Graceful Degradation

Reduce functionality instead of crashing.

Example:

If recommendation service fails:
Checkout still works


User experience is slightly reduced but system stays functional.

---

# 6. Example: Failure Handling in an E-commerce System

User places an order.

Flow:
User
↓
API Gateway
↓
Order Service
↓
Payment Service
↓
Inventory Service


Now suppose **payment service fails**.

Failure handling strategies:

1. Retry payment request
2. Timeout after 3 seconds
3. Use circuit breaker
4. Notify user
5. Allow retry later

System continues working.

---

# 7. Cascading Failures

A **cascading failure** occurs when one failure spreads to other services.

Example:
Database slow
↓
API response slow
↓
Threads blocked
↓
Entire system crashes


Failure handling prevents this using:

- Timeouts
- Circuit breakers
- Queue buffering

---

# 8. Failure Detection Techniques

Systems must detect failures quickly.

Common methods:

### Health Checks

Services expose health endpoints.

Example:
/health

Returns:
status: healthy


---

### Heartbeats

Services send periodic signals.

Example:
Service alive every 10 seconds


If heartbeat stops → service is down.

---

# 9. Real-World Example

### Netflix System

If one microservice fails:

- Circuit breaker stops requests
- Fallback responses are shown
- System degrades gracefully

Users may see:

- Fewer recommendations
- Slower loading

But **Netflix does not go down completely**.

---

# 10. Best Practices for Failure Handling

### Design for Failure

Assume failures will happen.

---

### Use Timeouts

Never allow infinite waiting.

---

### Implement Retries Carefully

Too many retries can overload systems.

---

### Use Circuit Breakers

Prevent cascading failures.

---

### Monitor and Alert

Detect failures quickly.

---

# 11. Failure Handling Architecture Example

Typical architecture:
Client
↓
API Gateway
↓
Load Balancer
↓
Microservices
↓
Retry + Timeout + Circuit Breaker
↓
Databases / Caches


Each layer includes **failure protection mechanisms**.

---

# 12. Interview Questions & Answers 🎤

### Q1. What is failure handling?

**Answer**

Failure handling refers to techniques used in system design to detect, manage, and recover from system failures without affecting overall system availability.

---

### Q2. Why is failure handling important?

**Answer**

Failures are unavoidable in distributed systems. Failure handling ensures systems remain resilient, available, and stable during errors.

---

### Q3. What is the circuit breaker pattern?

**Answer**

The circuit breaker pattern stops requests to a failing service after repeated failures to prevent system overload and cascading failures.

---

### Q4. What is exponential backoff?

**Answer**

Exponential backoff is a retry strategy where the wait time between retries increases exponentially.

Example:
1s → 2s → 4s → 8s


---

### Q5. What is graceful degradation?

**Answer**

Graceful degradation means reducing system functionality instead of failing completely when a component fails.

---

### Q6. What are cascading failures?

**Answer**

Cascading failures occur when one system failure spreads across multiple services causing widespread outages.

---

### Q7. What are common failure handling techniques?

**Answer**

- Retries
- Circuit breakers
- Timeouts
- Fallbacks
- Replication
- Load balancing

---

### Q8. How do systems detect failures?

**Answer**

Failures are detected using health checks, heartbeats, monitoring tools, and alert systems.

---

# 13. One-Line Summary

> **Failure handling ensures systems remain resilient and continue operating even when components fail.**
