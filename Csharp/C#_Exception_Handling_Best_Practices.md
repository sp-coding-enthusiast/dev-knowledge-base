# C# Exception Handling – Best Practices (Layman Explanation)

## Why exception handling matters (simple words)

Exceptions are **unexpected problems** that happen while your program is running.

Examples:

* File not found
* Database connection failed
* Divide by zero

If you don’t handle them properly:
❌ Application crashes
❌ Users see errors
❌ Debugging becomes painful

Good exception handling makes your app **stable, predictable, and professional**.

---

## What is an Exception?

An **exception** is like a **fire alarm** 🚨 in your code.

* Something went wrong
* Normal flow stops
* Control jumps to error-handling code

---

## Basic try-catch-finally

```csharp
try
{
    int result = 10 / 0; // problem here
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
finally
{
    Console.WriteLine("Cleanup work");
}
```

### Explanation:

* `try` → risky code
* `catch` → what to do if it fails
* `finally` → always runs (cleanup)

---

## Best Practices (Very Important)

## 1. Never use exceptions for normal flow

❌ Bad

```csharp
try
{
    int x = int.Parse(input);
}
catch
{
    x = 0;
}
```

✅ Good

```csharp
int x;
if (!int.TryParse(input, out x))
{
    x = 0;
}
```

**Why?** Exceptions are expensive and slow.

---

## 2. Catch specific exceptions, not Exception

❌ Bad

```csharp
catch (Exception)
{
}
```

✅ Good

```csharp
catch (DivideByZeroException ex)
{
}
catch (IOException ex)
{
}
```

**Why?** You know exactly what went wrong.

---

## 3. Never swallow exceptions

❌ Bad

```csharp
catch (Exception)
{
    // do nothing
}
```

✅ Good

```csharp
catch (Exception ex)
{
    logger.LogError(ex);
    throw;
}
```

**Why?** Silent failures are the worst bugs.

---

## 4. Use finally for cleanup

```csharp
FileStream fs = null;
try
{
    fs = new FileStream("file.txt", FileMode.Open);
}
finally
{
    fs?.Dispose();
}
```

Even if exception occurs, resources are released.

---

## 5. Prefer using statement

```csharp
using (var fs = new FileStream("file.txt", FileMode.Open))
{
    // work with file
}
```

Cleaner and safer than finally.

---

## 6. Do not throw generic Exception

❌ Bad

```csharp
throw new Exception("Invalid data");
```

✅ Good

```csharp
throw new ArgumentException("Invalid data");
```

Or create custom exception if needed.

---

## 7. Preserve stack trace when rethrowing

❌ Bad

```csharp
catch (Exception ex)
{
    throw ex;
}
```

✅ Good

```csharp
catch (Exception)
{
    throw;
}
```

**Why?** Keeps original error location.

---

## 8. Validate input early (Fail Fast)

```csharp
if (user == null)
    throw new ArgumentNullException(nameof(user));
```

Detect problems early instead of deep inside logic.

---

## Custom Exceptions

```csharp
public class PaymentFailedException : Exception
{
    public PaymentFailedException(string message) : base(message) { }
}
```

Use when:

* Domain-specific errors
* Business rules

---

## Exception Handling in Layers (Important)

| Layer   | Responsibility             |
| ------- | -------------------------- |
| UI      | Show user-friendly message |
| Service | Handle business exceptions |
| Data    | Throw technical exceptions |

❌ Don’t show stack traces to users

---

## Performance Tip

Exceptions are **slow**.

* Avoid in loops
* Avoid for validations
* Use conditions instead

---

## Interview Questions & Answers

### 1. What is an exception?

**Answer:**
An exception is a runtime error that disrupts normal program execution.

---

### 2. Difference between throw and throw ex?

**Answer:**
`throw` preserves stack trace, `throw ex` resets it.

---

### 3. When to use finally?

**Answer:**
For cleanup like closing files, database connections, releasing locks.

---

### 4. Should we catch Exception?

**Answer:**
Only at application boundaries (global handlers). Prefer specific exceptions elsewhere.

---

### 5. What is fail-fast?

**Answer:**
Validating input early and throwing exceptions immediately when invalid data is detected.

---

### 6. Are exceptions expensive?

**Answer:**
Yes. They should not be used for normal control flow.

---

## One-line interview summary

> Handle exceptions deliberately: catch specific ones, log them, clean resources properly, and never hide failures.

---

## Senior-level Insight

Good exception handling is not about catching everything — it’s about **knowing where to catch and where to let it fail**.
