# ASP.NET Core Dependency Injection (DI) Lifetimes

## Why DI lifetimes matter (simple words)

Dependency Injection helps your app **create and manage objects** automatically.

But an important question is:

> **How long should an object live?**

That is what **DI lifetimes** decide.

Wrong lifetime =
❌ Memory leaks
❌ Bugs
❌ Thread-safety issues

---

## Big picture (one line)

> **Singleton = one for the app**
> **Scoped = one per request**
> **Transient = new every time**

If you remember only this, you’re already ahead.

---

## Real-life analogy (easy to remember)

* **Singleton** → Office printer (shared by everyone)
* **Scoped** → Office meeting room (one per meeting)
* **Transient** → Disposable coffee cup (new each time)

---

## How DI works in ASP.NET Core

Services are registered in `Program.cs`:

```csharp
builder.Services.AddSingleton<IService, Service>();
builder.Services.AddScoped<IService, Service>();
builder.Services.AddTransient<IService, Service>();
```

ASP.NET Core creates and injects them automatically.

---

## 1️⃣ Singleton

### What it means

* **Only one instance** for the entire application lifetime
* Shared across all users and requests

```csharp
builder.Services.AddSingleton<CacheService>();
```

### When to use

✅ Configuration
✅ Caching
✅ Stateless services

### When NOT to use

❌ Services with user/request data
❌ Non-thread-safe code

### Common mistake

Using DbContext as Singleton ❌ (very dangerous)

---

## 2️⃣ Scoped

### What it means

* **One instance per HTTP request**
* Shared within the same request

```csharp
builder.Services.AddScoped<OrderService>();
```

### When to use

✅ DbContext
✅ Business services
✅ Unit of Work

### Why it’s popular

Most web apps should default to **Scoped**.

---

## 3️⃣ Transient

### What it means

* **New instance every time** it’s requested

```csharp
builder.Services.AddTransient<EmailService>();
```

### When to use

✅ Lightweight services
✅ Stateless helpers

### Caution

Too many transient objects = GC pressure

---

## Lifetime comparison (interview favorite)

| Lifetime  | Instance | Scope         | Typical use   |
| --------- | -------- | ------------- | ------------- |
| Singleton | One      | Entire app    | Cache, config |
| Scoped    | One      | Per request   | DbContext     |
| Transient | Many     | Per injection | Helpers       |

---

## Lifetime mismatch problem (VERY IMPORTANT)

### ❌ Bad

```csharp
builder.Services.AddSingleton<MyService>();
builder.Services.AddScoped<MyDbContext>();
```

Singleton depends on Scoped ❌

### Why it’s bad

* Scoped service may already be disposed
* Causes runtime exceptions

### Rule

> **Longer lifetime must NOT depend on shorter lifetime**

---

## Valid dependency direction

```
Singleton → Singleton
Scoped → Scoped / Singleton
Transient → Any
```

---

## Example: Correct usage

```csharp
builder.Services.AddScoped<AppDbContext>();
builder.Services.AddScoped<OrderService>();
```

---

## Background services & lifetimes

```csharp
builder.Services.AddHostedService<Worker>();
```

Hosted services are **Singleton by default**.

To use scoped services:

```csharp
using var scope = serviceProvider.CreateScope();
var db = scope.ServiceProvider.GetRequiredService<AppDbContext>();
```

---

## Common mistakes

❌ Making everything Singleton
❌ Using Transient for DbContext
❌ Ignoring thread safety
❌ Lifetime mismatch

---

## Interview Questions & Answers

### 1. What are DI lifetimes?

**Answer:**
They define how long a service instance lives in the application.

---

### 2. Default lifetime for DbContext?

**Answer:**
Scoped.

---

### 3. Can Singleton depend on Scoped?

**Answer:**
No, it causes lifetime mismatch issues.

---

### 4. When to use Transient?

**Answer:**
For lightweight, stateless services.

---

### 5. Which lifetime is most common?

**Answer:**
Scoped, for web applications.

---

## One-line interview summary

> Singleton lives for the app, Scoped lives per request, and Transient is created every time it’s requested.

---

## Senior-level Insight

Choosing the right DI lifetime is about **ownership and thread safety**, not convenience.
