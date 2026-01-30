# C# Important Concepts (Quick Reference)

This document covers **core C# concepts** you must know for **interviews, real-world development, and system design discussions**.

---

## 1. Basics of C#

* Strongly typed, object-oriented language
* Runs on **.NET runtime (CLR)**
* Garbage-collected
* Cross-platform with .NET Core / .NET

---

## 2. Data Types

* **Value Types**: int, double, bool, struct, enum
* **Reference Types**: class, string, array, object, interface
* `var` – compile-time type inference
* `dynamic` – runtime type resolution

---

## 3. OOP Concepts

* **Encapsulation** – data hiding using access modifiers
* **Inheritance** – reusability using `:`
* **Polymorphism** – method overriding and interfaces
* **Abstraction** – abstract classes and interfaces

Keywords:

* `class`, `interface`, `abstract`
* `virtual`, `override`, `sealed`

---

## 4. Access Modifiers

* `public`
* `private`
* `protected`
* `internal`
* `protected internal`

---

## 5. Constructors

* Default constructor
* Parameterized constructor
* Static constructor
* Private constructor

---

## 6. Interfaces vs Abstract Classes

* Interfaces support **multiple inheritance**
* Abstract classes can have **implementation + fields**
* Interfaces are preferred for **dependency injection**

---

## 7. Exception Handling

* `try`, `catch`, `finally`
* Custom exceptions
* Best practice: **don’t swallow exceptions**

---

## 8. Collections

* `List<T>`
* `Dictionary<TKey, TValue>`
* `Queue<T>`, `Stack<T>`
* `HashSet<T>`

Interfaces:

* `IEnumerable`
* `ICollection`
* `IList`

---

## 9. LINQ (Very Important)

* Query collections in a readable way

Common methods:

* `Where()`
* `Select()`
* `FirstOrDefault()`
* `Any()`
* `All()`
* `GroupBy()`
* `OrderBy()`

---

## 10. Delegates & Events

* Delegate = method reference
* Used heavily in events and callbacks

Types:

* `Func<>`
* `Action<>`
* `Predicate<>`

---

## 11. Async & Multithreading (High Priority)

* `async` / `await`
* `Task`, `Task<T>`
* Avoid `Task.Result` and `.Wait()`
* Use `ConfigureAwait(false)` in libraries

---

## 12. Memory Management

* Garbage Collector (GC)
* Managed vs unmanaged memory
* `IDisposable` and `using`

---

## 13. Dependency Injection (DI)

* Loose coupling
* Improves testability

Service lifetimes:

* Singleton
* Scoped
* Transient

---

## 14. File Handling

* `File`, `FileInfo`
* `Directory`, `DirectoryInfo`
* `StreamReader`, `StreamWriter`

---

## 15. .NET CLI Commands

```bash
dotnet new
dotnet build
dotnet run
dotnet test
dotnet publish
```

---

## 16. C# Advanced Concepts

* Records
* Immutability
* Span & Memory
* ValueTask
* Pattern matching

---

## 17. Best Practices

* Follow **SOLID principles**
* Prefer async APIs
* Avoid blocking calls
* Write unit tests
* Use logging properly

---

## 18. Interview-Focused Topics (Must Prepare)

* `IEnumerable vs IQueryable`
* `ref vs out`
* `struct vs class`
* `string vs StringBuilder`
* Boxing & Unboxing
* Deadlock scenarios

---

## 19. C# in Enterprise Applications

* ASP.NET Core
* Web APIs
* Microservices
* Azure Functions
* Event-driven architecture

---

## 20. Final Advice

> If you master **OOP + LINQ + async/await + DI**, you are already ahead of 80% of candidates.

---

**End of Document**
