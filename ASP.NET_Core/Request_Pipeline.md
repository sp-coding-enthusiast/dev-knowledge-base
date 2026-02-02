# ASP.NET Core Request Pipeline (Layman Explanation)

## Why the request pipeline matters (simple words)

Every time a user hits your API or website, a **request** comes in.

ASP.NET Core does not handle it magically.
It passes the request through a **pipeline** — a sequence of steps.

Think of it like an **airport security process** ✈️:

* Entry check
* Security scan
* Passport control
* Boarding gate

Each step decides:

* Let the request continue
* Modify it
* Or stop it

---

## What is the Request Pipeline?

The **request pipeline** is an **ordered chain of middleware components**.

Each middleware can:

* Inspect the request
* Do some work
* Pass it to the next middleware
* Or short-circuit the pipeline

---

## High-level flow

```
Request
   ↓
Middleware 1
   ↓
Middleware 2
   ↓
Middleware 3
   ↓
Endpoint (Controller / Minimal API)
   ↓
Response (goes back through middleware)
```

---

## What is Middleware?

Middleware is a **piece of code** that runs:

* Before the next component
* After the next component

```csharp
public async Task InvokeAsync(HttpContext context, RequestDelegate next)
{
    // Before
    await next(context);
    // After
}
```

---

## Real-life analogy

Imagine a factory conveyor belt:

* Each station does one job
* The product moves step by step

Middleware works the same way.

---

## Pipeline Order Matters (VERY IMPORTANT)

Middleware executes in the **order it is added**.

Wrong order = bugs or security issues.

---

## Common Built-in Middleware

* Exception handling
* HTTPS redirection
* Static files
* Routing
* Authentication
* Authorization
* Endpoints

---

## Typical ASP.NET Core Pipeline

```csharp
var app = builder.Build();

app.UseExceptionHandler("/error");
app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthentication();
app.UseAuthorization();

app.MapControllers();

app.Run();
```

---

## Step-by-step explanation

### 1️⃣ Exception Handling Middleware

```csharp
app.UseExceptionHandler("/error");
```

* Catches unhandled exceptions
* Prevents app crash
* Should be **at the top**

---

### 2️⃣ HTTPS Redirection

```csharp
app.UseHttpsRedirection();
```

* Redirects HTTP → HTTPS
* Improves security

---

### 3️⃣ Static Files

```csharp
app.UseStaticFiles();
```

* Serves CSS, JS, images
* Short-circuits pipeline if file found

---

### 4️⃣ Routing

```csharp
app.UseRouting();
```

* Matches URL to endpoint
* Does NOT execute controller

---

### 5️⃣ Authentication

```csharp
app.UseAuthentication();
```

* Identifies the user
* Reads tokens/cookies

---

### 6️⃣ Authorization

```csharp
app.UseAuthorization();
```

* Checks permissions
* Must be AFTER authentication

---

### 7️⃣ Endpoint Execution

```csharp
app.MapControllers();
```

* Executes controller or API endpoint

---

## Custom Middleware Example

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine("Request started");
    await next();
    Console.WriteLine("Request finished");
});
```

---

## Short-circuiting the pipeline

```csharp
app.Use(async (context, next) =>
{
    if (!context.Request.Headers.ContainsKey("X-API-KEY"))
    {
        context.Response.StatusCode = 401;
        return; // pipeline stops here
    }
    await next();
});
```

---

## app.Use vs app.Run vs app.Map

| Method | Purpose                        |
| ------ | ------------------------------ |
| Use    | Adds middleware and calls next |
| Run    | Terminal middleware (no next)  |
| Map    | Branch pipeline based on path  |

---

## Request vs Response flow

* Request flows **top → bottom**
* Response flows **bottom → top**

Like going down stairs and coming back up.

---

## Common Mistakes

❌ Wrong middleware order
❌ Missing UseRouting
❌ Authorization before Authentication
❌ Doing heavy work in middleware

---

## Performance Note

* Middleware runs for **every request**
* Keep middleware lightweight

---

## Interview Questions & Answers

### 1. What is ASP.NET Core request pipeline?

**Answer:**
It is an ordered sequence of middleware that handles HTTP requests and responses.

---

### 2. Why does middleware order matter?

**Answer:**
Because each middleware depends on the previous one, and incorrect order can break routing, security, or performance.

---

### 3. Difference between Use and Run?

**Answer:**
Use can call the next middleware; Run ends the pipeline.

---

### 4. What is short-circuiting?

**Answer:**
Stopping the pipeline early without calling the next middleware.

---

### 5. Where should authentication and authorization go?

**Answer:**
After routing and before endpoint execution.

---

## One-line interview summary

> ASP.NET Core processes requests through an ordered middleware pipeline where each component can inspect, modify, or terminate the request.

---

## Senior-level Insight

A clean pipeline design keeps middleware small, ordered correctly, and focused on a single responsibility.
