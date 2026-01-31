# .NET Memory Management

## Stack, Heap, Garbage Collector (GC) & Large Object Heap (LOH)

---

## Big Picture (Layman View)

Think of memory like **storage in your house**:

* **Stack** → Temporary desk space (very fast)
* **Heap** → Storage room (bigger, flexible)
* **GC** → House cleaner
* **LOH** → Warehouse for very large items

---

## Stack Memory

### What is Stack?

Stack is used for:

* Method calls
* Local variables
* Value types (mostly)

### Key Characteristics

* Very fast
* Memory is allocated and released automatically
* Follows **LIFO** (Last In, First Out)

### Example

```csharp
void Calculate()
{
    int x = 10;   // stored in stack
    int y = 20;   // stored in stack
}
```

When the method ends, stack memory is cleared automatically.

> Stack memory is short-lived and self-cleaning.

---

## Heap Memory

### What is Heap?

Heap stores:

* Objects created using `new`
* Reference types (class, array, string, etc.)

### Example

```csharp
class Person
{
    public string Name;
}

Person p = new Person(); // object stored in heap
```

The variable `p` is on stack, but the actual object is on heap.

### Characteristics

* Slower than stack
* Memory is not freed automatically
* Managed by Garbage Collector

---

## Garbage Collector (GC)

### What is GC?

**GC automatically frees heap memory that is no longer used.**

### Layman Explanation

> GC is like a cleaner who removes unused objects from memory so your application does not run out of space.

You **do not manually delete objects** in .NET.

---

## How GC Works (Simple Steps)

1. GC checks which objects are still in use
2. Objects that are not referenced are marked as garbage
3. GC removes unused objects
4. Memory is compacted for reuse

---

## Generational GC (Very Important)

GC divides heap objects into **generations** based on age.

| Generation | Meaning      | Example           |
| ---------- | ------------ | ----------------- |
| Gen 0      | New objects  | Temporary objects |
| Gen 1      | Medium-lived | Cached objects    |
| Gen 2      | Long-lived   | App-wide data     |

> Most objects die young → GC optimizes for this

---

## Example of GC in Action

```csharp
void Test()
{
    Person p = new Person();
}
```

After method execution:

* `p` goes out of scope
* Object becomes unreachable
* GC eventually removes it

---

## Large Object Heap (LOH)

### What is LOH?

Objects **larger than 85 KB** are stored in LOH.

### Examples

```csharp
byte[] buffer = new byte[100000]; // goes to LOH
```

### Characteristics

* Separate heap area
* Not compacted by default
* GC is expensive

> LOH is like a warehouse for large items.

---

## Stack vs Heap (Interview Table)

| Feature  | Stack           | Heap       |
| -------- | --------------- | ---------- |
| Speed    | Very fast       | Slower     |
| Storage  | Local variables | Objects    |
| Cleanup  | Automatic       | GC managed |
| Lifetime | Short           | Long       |

---

## Common GC Triggers

* Heap memory pressure
* Explicit `GC.Collect()` (not recommended)
* Application idle time

---

## Best Practices

* Avoid unnecessary object creation
* Reuse objects when possible
* Avoid frequent large object allocations
* Do not call `GC.Collect()` manually

---

## Interview-Friendly Summary

> In .NET, stack memory stores method-level data and is automatically cleared. Heap memory stores objects and is managed by the Garbage Collector. The GC automatically removes unused objects using a generational approach for better performance. Large objects are stored separately in the Large Object Heap.

---

## One-Line Summary

**Stack is fast and short-lived, Heap stores objects, GC cleans unused memory, and LOH handles large allocations.**
