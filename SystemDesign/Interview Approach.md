# System Design – Design Interview Approach

## 1. What is a System Design Interview?

In simple words, a system design interview checks how you think when building a large system.

It is NOT about writing code.
It is about:

* Understanding the problem
* Making smart decisions
* Explaining trade-offs
* Designing scalable systems

Example questions:

* Design a URL shortener like TinyURL
* Design a chat system like WhatsApp
* Design a video streaming system like YouTube

The interviewer wants to see your thinking process more than the final answer.

---

# 2. Step-by-Step Approach (Very Important)

Follow this structure in every system design interview.

## Step 1: Clarify Requirements (Never Skip This)

Ask questions before jumping to solution.

### Functional Requirements (What system should do)

Example for URL shortener:

* User can paste long URL
* System generates short URL
* When user clicks short URL → redirect to original

### Non-Functional Requirements (How system should behave)

* Should handle 10 million users?
* Should it be highly available?
* How fast should response be?
* Is data durability important?

This step shows maturity.

---

## Step 2: Estimate Scale (Back-of-the-envelope calculation)

Interviewers love this.

Example:
If 10 million users create 5 URLs per day:

10M × 5 = 50M URLs per day

Storage estimate:
If each URL record is 500 bytes:
50M × 500 bytes ≈ 25 GB per day

This helps you decide:

* Database type
* Sharding need
* Caching strategy

Even rough math is fine.

---

## Step 3: High-Level Design

Draw main components.

For URL shortener:

* Client (Browser / App)
* Load Balancer
* Application Servers
* Database
* Cache

Explain request flow:
User → Load Balancer → App Server → DB → Response

Keep it simple first.

---

## Step 4: Deep Dive (Important Parts)

Now go deeper into critical areas.

For example:

### 1. Database Choice

* SQL (structured data, relationships)
* NoSQL (high scale, flexible schema)

Explain WHY.

Example:
For URL shortener, NoSQL key-value store is good because lookup is simple.

### 2. Caching

* Use Redis
* Cache frequently accessed URLs

Why?
To reduce database load and improve speed.

### 3. Scaling

Horizontal scaling:
Add more servers behind load balancer.

Database scaling:

* Read replicas
* Sharding

Explain trade-offs.

---

## Step 5: Bottlenecks & Improvements

Always discuss:

* Single point of failure?
* What if database crashes?
* How to improve availability?

Solutions:

* Replication
* Multi-region deployment
* Failover strategy

This shows senior-level thinking.

---

# 3. Example: Design a Chat System (Layman Version)

### Requirements

* Send message
* Receive message instantly
* Store chat history

### High-Level Components

* Mobile App
* WebSocket Server
* Message Queue
* Database

### Flow

User A sends message → Server → Message Queue → User B receives instantly.

If User B offline:
Message stored in DB → Delivered later.

### Key Concepts

* WebSocket for real-time communication
* Message Queue for reliability
* Database for persistence

---

# 4. Common Interview Questions & How to Answer

## Q1: How do you scale this system?

Answer structure:

* Add load balancer
* Horizontal scaling
* Caching
* Database sharding

## Q2: SQL or NoSQL?

Answer:
Depends on:

* Data structure
* Consistency needs
* Query complexity

Explain trade-off. No one answer is always correct.

## Q3: How do you handle millions of users?

Answer:

* Horizontal scaling
* CDN
* Caching
* Partitioning
* Async processing

---

# 5. Golden Rules for System Design Interview

1. Never jump into solution immediately.
2. Always clarify requirements first.
3. Think aloud clearly.
4. Keep design simple first.
5. Discuss trade-offs.
6. Talk about scaling and failure handling.

Interviewers care about structured thinking more than perfect architecture.

---

# 6. Common Mistakes (Avoid These)

* Starting without asking questions
* Overengineering
* Forgetting scale
* Ignoring failures
* Not explaining trade-offs

---

# 7. Final Interview Strategy

If you feel stuck:

* Go back to requirements
* Simplify design
* Build step by step

Confidence + clarity beats complexity.

---

# Summary

System design interview is about:

* Structured thinking
* Clear communication
* Trade-off discussion
* Scalability awareness

Practice 8–10 common problems and follow same framework every time.

That consistency is what makes candidates strong.
