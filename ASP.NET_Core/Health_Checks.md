# ASP.NET Core – Health Checks

## 1. What are Health Checks? (Layman Explanation)

**Health checks** answer one simple question:
👉 *Is my application healthy and ready to serve requests?*

Instead of guessing, systems can **ask your app directly**.

---

## 2. Real-Life Analogy

Think of a **car dashboard**:

* Engine light ❌ → car has problem
* All lights OK ✅ → car is healthy

Health checks are the **dashboard of your application**.

---

## 3. Why Health Checks Are Important

Without health checks:

* Monitoring systems are blind
* Load balancers send traffic to broken apps
* Failures detected too late

With health checks:

* Early failure detection
* Auto-restart unhealthy services
* Better reliability

---

## 4. What Does “Healthy” Mean?

An app is healthy if:

* App is running
* Database is reachable
* External services are available
* Disk / memory is OK

---

## 5. Where Are Health Checks Used?

* Load balancers
* Kubernetes
* Azure App Service
* Monitoring tools

---

## 6. Health Checks in ASP.NET Core

ASP.NET Core provides **built-in health check support**.

---

## 7. Basic Health Check Setup

### Register Health Checks

```csharp
builder.Services.AddHealthChecks();
```

### Map Health Endpoint

```csharp
app.MapHealthChecks("/health");
```

### Result

```
GET /health → 200 OK
```

---

## 8. Database Health Check Example

```csharp
builder.Services.AddHealthChecks()
    .AddSqlServer(
        connectionString: "Server=.;Database=AppDb;Trusted_Connection=True;",
        name: "sql-database");
```

✔ Fails if DB is down

---

## 9. Custom Health Check (Most Asked in Interviews)

### Step 1: Create Health Check

```csharp
public class ApiHealthCheck : IHealthCheck
{
    public Task<HealthCheckResult> CheckHealthAsync(
        HealthCheckContext context,
        CancellationToken cancellationToken = default)
    {
        bool apiUp = true; // custom logic

        return apiUp
            ? Task.FromResult(HealthCheckResult.Healthy("API is OK"))
            : Task.FromResult(HealthCheckResult.Unhealthy("API is Down"));
    }
}
```

---

### Step 2: Register Custom Health Check

```csharp
builder.Services.AddHealthChecks()
    .AddCheck<ApiHealthCheck>("custom-api");
```

---

## 10. Health Check Status Values

| Status    | Meaning               |
| --------- | --------------------- |
| Healthy   | Everything OK         |
| Degraded  | App works but limited |
| Unhealthy | App is broken         |

---

## 11. Readiness vs Liveness (Kubernetes Favorite)

### Liveness Check

* Is app alive?
* If failed → restart app

### Readiness Check

* Is app ready to receive traffic?
* If failed → stop traffic

---

## 12. Separate Endpoints Example

```csharp
app.MapHealthChecks("/health/live", new HealthCheckOptions
{
    Predicate = _ => false
});

app.MapHealthChecks("/health/ready", new HealthCheckOptions
{
    Predicate = check => check.Name.Contains("sql")
});
```

---

## 13. Health Check Response Codes

| Status    | HTTP Code |
| --------- | --------- |
| Healthy   | 200       |
| Degraded  | 200       |
| Unhealthy | 503       |

---

## 14. Health Checks vs Monitoring (Interview)

| Health Checks   | Monitoring      |
| --------------- | --------------- |
| Current state   | Historical data |
| Simple          | Detailed        |
| Used by systems | Used by humans  |

---

## 15. Common Interview Questions & Answers

### Q1. What are health checks?

**Answer:**
Health checks indicate whether an application and its dependencies are functioning correctly.

---

### Q2. Difference between liveness and readiness?

**Answer:**
Liveness checks if app is alive; readiness checks if it can accept traffic.

---

### Q3. What HTTP code is returned when unhealthy?

**Answer:**
503 Service Unavailable.

---

### Q4. Can we create custom health checks?

**Answer:**
Yes, by implementing `IHealthCheck`.

---

### Q5. Are health checks expensive?

**Answer:**
No, they should be lightweight and fast.

---

## 16. Common Mistakes

* Heavy DB queries in health checks
* Exposing sensitive info
* Single health endpoint for everything

---

## 17. Best Practices

* Keep health checks lightweight
* Separate liveness & readiness
* Secure health endpoints

---

## 18. Key Takeaways

* Health checks improve reliability
* Built-in support in ASP.NET Core
* Critical for cloud & containers
* Interview favorite topic

---

✅ **Interview One-Liner:**
"Health checks allow systems to automatically verify whether an application and its dependencies are healthy."
