# ASP.NET Core – API Versioning

## 1. What is API Versioning? (Layman Explanation)

**API Versioning** means:
👉 Allowing **multiple versions of the same API** to exist so that **old clients don’t break** when you make changes.

Simple idea:

* Old mobile app → uses old API
* New mobile app → uses new API
* Both should work at the same time

---

## 2. Real-Life Analogy

Think of **mobile phone chargers**:

* Old phones → Micro USB
* New phones → Type-C

You don’t break old phones when new chargers come.

API versioning works the same way.

---

## 3. Why API Versioning is Important

Without versioning:

* Any change can break clients
* Production outages
* Angry users

With versioning:

* Safe evolution of APIs
* Backward compatibility
* Controlled rollout

---

## 4. When Do You Need Versioning?

You need versioning when you:

* Change response structure
* Remove fields
* Change business logic
* Rename endpoints

---

## 5. Common API Versioning Strategies

### 1️⃣ URL Versioning (Most Common)

```
/api/v1/users
/api/v2/users
```

✔ Easy to understand
❌ URL changes

---

### 2️⃣ Query String Versioning

```
/api/users?api-version=1.0
```

✔ Simple
❌ Easy to forget version

---

### 3️⃣ Header Versioning

```
api-version: 1.0
```

✔ Clean URLs
❌ Harder to debug

---

### 4️⃣ Media Type Versioning

```
Accept: application/json;v=1
```

✔ Pure REST
❌ Complex

---

## 6. API Versioning in ASP.NET Core

ASP.NET Core provides **Microsoft.AspNetCore.Mvc.Versioning** package.

---

## 7. URL Versioning – Example

### Install Package

```
dotnet add package Microsoft.AspNetCore.Mvc.Versioning
```

---

### Configure Versioning

```csharp
builder.Services.AddApiVersioning(options =>
{
    options.DefaultApiVersion = new ApiVersion(1, 0);
    options.AssumeDefaultVersionWhenUnspecified = true;
    options.ReportApiVersions = true;
});
```

---

### Controller – Version 1

```csharp
[ApiVersion("1.0")]
[Route("api/v{version:apiVersion}/users")]
[ApiController]
public class UsersV1Controller : ControllerBase
{
    [HttpGet]
    public IActionResult Get() => Ok("Users V1");
}
```

---

### Controller – Version 2

```csharp
[ApiVersion("2.0")]
[Route("api/v{version:apiVersion}/users")]
[ApiController]
public class UsersV2Controller : ControllerBase
{
    [HttpGet]
    public IActionResult Get() => Ok("Users V2 with more fields");
}
```

---

## 8. Query String Versioning – Example

```csharp
options.ApiVersionReader = new QueryStringApiVersionReader("api-version");
```

Request:

```
/api/users?api-version=2.0
```

---

## 9. Header Versioning – Example

```csharp
options.ApiVersionReader = new HeaderApiVersionReader("x-api-version");
```

Request Header:

```
x-api-version: 1.0
```

---

## 10. What is Default API Version?

If client doesn’t specify version:

* Default version is used
* Prevents breaking old clients

---

## 11. Deprecating an API Version

```csharp
[ApiVersion("1.0", Deprecated = true)]
```

✔ Clients get warning headers

---

## 12. Versioning Best Practices

* Don’t version too early
* Version only when breaking changes happen
* Keep versions minimal
* Document deprecated versions

---

## 13. API Versioning vs API Evolution (Interview)

| Versioning                | Evolution                 |
| ------------------------- | ------------------------- |
| Multiple versions         | Same version grows        |
| Used for breaking changes | Used for additive changes |

---

## 14. Common Interview Questions & Answers

### Q1. Why API versioning is needed?

**Answer:**
To avoid breaking existing clients when APIs change.

---

### Q2. Which API versioning approach is best?

**Answer:**
URL versioning is the most commonly used due to simplicity and visibility.

---

### Q3. Can we avoid API versioning?

**Answer:**
Yes, if changes are backward compatible.

---

### Q4. What happens if version is not specified?

**Answer:**
Default API version is used if configured.

---

### Q5. How do you deprecate an API?

**Answer:**
Mark version as deprecated and inform clients before removal.

---

## 15. Common Mistakes

* Versioning every small change
* Removing versions without notice
* Poor documentation

---

## 16. Key Takeaways

* API versioning protects clients
* Required for breaking changes
* ASP.NET Core supports multiple strategies
* URL versioning is most popular

---

✅ **Interview One-Liner:**
"API versioning allows safe evolution of APIs without breaking existing consumers."
