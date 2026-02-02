# ASP.NET Core: Middleware vs Filters (Layman Explanation)

## Why this topic matters

This is a **very common interview question** because many developers confuse these two.

Both **Middleware** and **Filters**:

* Run during request processing
* Can execute code before and after logic

But they operate at **different levels** of the ASP.NET Core pipeline.

---

## Big-picture difference (one line)

> **Middleware works at the HTTP pipeline level, Filters work at the MVC/action level.**

Keep this sentence in mind.

---

## Real-life analogy (easy to remember)

### Middleware = Airport security

* Every passenger goes through it
* Happens before reaching the gate
* Applies to **all flights**

### Filters = Boarding gate checks

* Only for specific flights
* Happens just before boarding
* Applies to **specific actions/controllers**

---

## Middleware

### What is Middleware?

Middleware is a component that handles **every HTTP request** that flows through the ASP.NET Core pipeline.

It runs **before routing and controllers**.

---

### Middleware execution flow

```
Request
 ↓
Middleware 1
 ↓
Middleware 2
 ↓
Routing
 ↓
Controller / Endpoint
```

---

### Middleware example

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine("Request started");
    await next();
    Console.WriteLine("Request finished");
});
```

### When to use Middleware

✅ Logging
✅ Authentication
✅ Exception handling
✅ CORS
✅ HTTPS redirection

---

## Filters

### What are Filters?

Filters run **inside MVC**, around controller and action execution.

They apply **only when a controller/action is selected**.

---

### Filter execution flow

```
Middleware
 ↓
Routing
 ↓
Filter
 ↓
Controller Action
 ↓
Filter
```

---

### Types of Filters

* Authorization filters
* Resource filters
* Action filters
* Exception filters
* Result filters

---

### Action Filter example

```csharp
public class LogActionFilter : IActionFilter
{
    public void OnActionExecuting(ActionExecutingContext context)
    {
        Console.WriteLine("Before action");
    }

    public void OnActionExecuted(ActionExecutedContext context)
    {
        Console.WriteLine("After action");
    }
}
```

Apply it:

```csharp
[ServiceFilter(typeof(LogActionFilter))]
public IActionResult Get()
{
    return Ok();
}
```

---

## Key Differences (Most Important)

| Aspect                | Middleware         | Filters                      |
| --------------------- | ------------------ | ---------------------------- |
| Level                 | HTTP pipeline      | MVC pipeline                 |
| Runs for              | Every request      | Selected actions/controllers |
| Framework dependency  | Framework-agnostic | MVC-specific                 |
| Access to action args | ❌ No               | ✅ Yes                        |
| Order control         | Program.cs order   | Filter order                 |

---

## When NOT to use each

### Don’t use Middleware when:

❌ You need action parameters
❌ Logic applies only to specific endpoints

### Don’t use Filters when:

❌ Logic must apply globally
❌ You need raw HTTP control

---

## Performance perspective

* Middleware runs for **every request** → keep it lightweight
* Filters run only when MVC is involved

---

## Common Mistakes

❌ Using filters for logging everything
❌ Putting business logic in middleware
❌ Confusing authorization filters with authentication middleware

---

## Interview Questions & Answers

### 1. Middleware vs Filters?

**Answer:**
Middleware handles requests at the HTTP pipeline level, while filters run within MVC around controller actions.

---

### 2. Can filters replace middleware?

**Answer:**
No. Filters only run when MVC is used, middleware works for all requests.

---

### 3. Where does authentication happen?

**Answer:**
Authentication is typically done in middleware; authorization can be done using filters.

---

### 4. Can middleware access action parameters?

**Answer:**
No, middleware runs before routing and action execution.

---

## One-line interview summary

> Use middleware for cross-cutting HTTP concerns and filters for MVC-specific logic around controllers and actions.

---

## Senior-level Insight

A clean ASP.NET Core application keeps middleware minimal and global, and uses filters for controller-specific behavior.
