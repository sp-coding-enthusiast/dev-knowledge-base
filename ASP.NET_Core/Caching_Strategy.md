# ASP.NET Core – Caching Strategies

## 1. What is Caching? (Layman Explanation)

**Caching** means:
👉 *Storing frequently used data in a fast place so you don’t have to calculate or fetch it again.*

Simple idea:

* First request → slow
* Next requests → fast (from cache)

---

## 2. Real-Life Analogy

Think of a **food delivery app**:

* First time you open restaurant list → loads slowly
* Next time → opens instantly

Why?
Because data is cached.

---

## 3. Why Caching Is Important

Without caching:

* Repeated database calls
* Slow APIs
* High server cost

With caching:

* Faster response time
* Reduced database load
* Better scalability

---

## 4. Where Can We Cache?

| Location       | Speed   | Example       |
| -------------- | ------- | ------------- |
| In-Memory      | Fastest | Same server   |
| Distributed    | Fast    | Redis         |
| Client-side    | Fast    | Browser cache |
| Response cache | Medium  | HTTP cache    |

---

## 5. Types of Caching in ASP.NET Core

1. In-Memory Caching
2. Distributed Caching
3. Response Caching
4. Output Caching (.NET 7+)

---

## 6. In-Memory Caching (Simple & Fast)

Stores data in server memory.

### Setup

```csharp
builder.Services.AddMemoryCache();
```

### Example

```csharp
public class ProductService
{
    private readonly IMemoryCache _cache;

    public ProductService(IMemoryCache cache)
    {
        _cache = cache;
    }

    public List<string> GetProducts()
    {
        return _cache.GetOrCreate("products", entry =>
        {
            entry.AbsoluteExpirationRelativeToNow = TimeSpan.FromMinutes(5);
            return LoadFromDatabase();
        });
    }
}
```

✔ Very fast
❌ Not shared across servers

---

## 7. Distributed Caching (Scalable)

Cache shared across multiple servers.

Common tool: **Redis**

### Setup

```csharp
builder.Services.AddStackExchangeRedisCache(options =>
{
    options.Configuration = "localhost:6379";
});
```

### Example

```csharp
var data = await cache.GetStringAsync("products");

if (data == null)
{
    data = GetFromDb();
    await cache.SetStringAsync("products", data);
}
```

✔ Works in load-balanced systems
❌ Slightly slower than memory cache

---

## 8. Response Caching (HTTP Level)

Caches full HTTP responses.

### Enable Middleware

```csharp
app.UseResponseCaching();
```

### Controller

```csharp
[ResponseCache(Duration = 60)]
public IActionResult GetData() => Ok("Cached Response");
```

✔ Reduces API execution
❌ Not suitable for personalized data

---

## 9. Output Caching (.NET 7+)

Modern replacement for response caching.

### Setup

```csharp
builder.Services.AddOutputCache();
app.UseOutputCache();
```

### Example

```csharp
[OutputCache(Duration = 60)]
public IActionResult GetProducts() => Ok("Cached Output");
```

✔ More powerful
✔ Per-user support

---

## 10. Cache Expiration Strategies

| Strategy | Meaning                       |
| -------- | ----------------------------- |
| Absolute | Expires at fixed time         |
| Sliding  | Resets timer on access        |
| Eviction | Removed under memory pressure |

---

## 11. Cache Invalidation (Hard Part)

Cache must be cleared when data changes.

Strategies:

* Time-based expiry
* Manual removal
* Event-based invalidation

---

## 12. Caching vs Data Consistency

More caching = Faster APIs
Less caching = Fresh data

Balance is key.

---

## 13. Caching vs Session (Interview)

| Caching     | Session       |
| ----------- | ------------- |
| Performance | User state    |
| Shared      | User-specific |
| Stateless   | Stateful      |

---

## 14. Common Interview Questions & Answers

### Q1. What is caching?

**Answer:**
Caching stores frequently accessed data to improve performance and scalability.

---

### Q2. Difference between in-memory and distributed cache?

**Answer:**
In-memory cache is local and fast, distributed cache is shared and scalable.

---

### Q3. What is output caching?

**Answer:**
It caches the final API response to avoid re-executing the request pipeline.

---

### Q4. Biggest challenge in caching?

**Answer:**
Cache invalidation and data consistency.

---

### Q5. When should caching NOT be used?

**Answer:**
For highly dynamic or user-specific sensitive data.

---

## 15. Common Mistakes

* Caching user-specific data globally
* No cache expiry
* Over-caching everything

---

## 16. Best Practices

* Cache read-heavy data
* Use distributed cache in production
* Set proper expiration
* Monitor cache hit ratio

---

## 17. Key Takeaways

* Caching boosts performance
* Multiple caching strategies exist
* Output cache is modern choice
* Invalidation is critical

---

✅ **Interview One-Liner:**
"Caching improves API performance by storing frequently accessed data and reducing repeated work."
