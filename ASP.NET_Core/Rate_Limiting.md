# ASP.NET Core – Rate Limiting

## 1. What is Rate Limiting? (Layman Explanation)

**Rate limiting** means:
👉 *Limiting how many requests a user or client can make to an API within a given time.*

Simple idea:

* Too many requests → system slows or crashes
* Rate limiting → protects the system

---

## 2. Real-Life Analogy

Think of an **ATM machine**:

* You can’t withdraw money unlimited times per minute
* Bank limits attempts to prevent misuse

Rate limiting does the same for APIs.

---

## 3. Why Rate Limiting Is Important

Without rate limiting:

* API abuse
* DDoS attacks
* Server overload

With rate limiting:

* Fair usage
* Better performance
* Improved security

---

## 4. Common Use Cases

* Public APIs
* Login endpoints
* OTP / password reset APIs
* Expensive database calls

---

## 5. Common Rate Limiting Strategies

### 1️⃣ Fixed Window

* Allow X requests per time window
* Counter resets after window

Example:

* 100 requests per minute

❌ Burst issue at window edges

---

### 2️⃣ Sliding Window

* Window moves continuously
* More accurate control

✔ Smoother limiting

---

### 3️⃣ Token Bucket (Most Popular)

* Tokens added at fixed rate
* Each request consumes a token

✔ Handles bursts well

---

### 4️⃣ Leaky Bucket

* Requests processed at constant rate
* Extra requests queued or dropped

---

## 6. Rate Limiting in ASP.NET Core (.NET 7+)

ASP.NET Core has **built-in rate limiting middleware**.

---

## 7. Basic Rate Limiting Setup

```csharp
builder.Services.AddRateLimiter(options =>
{
    options.AddFixedWindowLimiter("fixed", opt =>
    {
        opt.Window = TimeSpan.FromMinutes(1);
        opt.PermitLimit = 100;
    });
});
```

---

## 8. Enable Rate Limiting Middleware

```csharp
app.UseRateLimiter();
```

---

## 9. Apply Rate Limiting to Endpoints

```csharp
app.MapGet("/api/data", () => "Hello")
   .RequireRateLimiting("fixed");
```

---

## 10. Token Bucket Example

```csharp
options.AddTokenBucketLimiter("token", opt =>
{
    opt.TokenLimit = 10;
    opt.QueueLimit = 2;
    opt.ReplenishmentPeriod = TimeSpan.FromSeconds(10);
    opt.TokensPerPeriod = 5;
    opt.AutoReplenishment = true;
});
```

---

## 11. What Happens When Limit Is Exceeded?

* Request is rejected
* API returns:

```
429 Too Many Requests
```

Optional headers:

* Retry-After

---

## 12. Per-User / Per-IP Rate Limiting

Rate limiting can be applied based on:

* IP address
* User ID
* API key

---

## 13. Global vs Endpoint-Level Limiting

| Global              | Endpoint-Level |
| ------------------- | -------------- |
| Applies to all APIs | Specific APIs  |
| Simple              | Flexible       |

---

## 14. Rate Limiting vs Throttling (Interview)

| Rate Limiting    | Throttling        |
| ---------------- | ----------------- |
| Hard limit       | Slows requests    |
| Rejects requests | Delays processing |

---

## 15. Common Interview Questions & Answers

### Q1. What is rate limiting?

**Answer:**
Rate limiting restricts the number of API requests a client can make within a time period.

---

### Q2. Why rate limiting is important?

**Answer:**
To prevent abuse, protect system resources, and ensure fair usage.

---

### Q3. Which HTTP status code is returned?

**Answer:**
429 Too Many Requests.

---

### Q4. What is the best rate limiting strategy?

**Answer:**
Token bucket is commonly preferred due to burst handling.

---

### Q5. Can rate limiting be applied per user?

**Answer:**
Yes, using IP, user identity, or API keys.

---

## 16. Common Mistakes

* No rate limiting on public APIs
* Same limits for all endpoints
* Ignoring retry headers

---

## 17. Best Practices

* Apply stricter limits to sensitive endpoints
* Log rate-limit violations
* Combine with authentication

---

## 18. Key Takeaways

* Rate limiting protects APIs
* Built-in support in ASP.NET Core
* Token bucket is most flexible
* Always return proper status codes

---

✅ **Interview One-Liner:**
"Rate limiting protects APIs by restricting how frequently clients can make requests."
