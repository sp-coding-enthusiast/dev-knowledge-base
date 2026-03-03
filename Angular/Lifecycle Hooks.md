# Angular – Lifecycle Hooks (Layman Explanation + Examples + Interview Q&A)

## 1. What Are Lifecycle Hooks? (Simple Explanation)

Lifecycle hooks are special methods in Angular that get executed at different stages of a component’s life.

Think of a component like a human being:

* It is **born** (created)
* It **grows** (updates when data changes)
* It **lives** (responds to user interaction)
* It **dies** (removed from the screen)

Lifecycle hooks allow you to run code at each of these stages.

---

## 2. Why Are Lifecycle Hooks Important?

They help you:

* Fetch data when component loads
* Respond to input changes
* Work with DOM after rendering
* Clean up memory before component is destroyed

Without lifecycle hooks, managing component behavior would be difficult.

---

## 3. Complete Lifecycle Flow (Order of Execution)

Here is the common execution order:

1. constructor()
2. ngOnChanges()
3. ngOnInit()
4. ngDoCheck()
5. ngAfterContentInit()
6. ngAfterContentChecked()
7. ngAfterViewInit()
8. ngAfterViewChecked()
9. ngOnDestroy()

You don’t need all of them every time — use only when needed.

---

## 4. Important Lifecycle Hooks Explained with Examples

### 1️⃣ constructor()

* Runs when component class is created
* Used for dependency injection
* Avoid writing heavy logic here

```ts
constructor() {
  console.log('Component Created');
}
```

---

### 2️⃣ ngOnInit()

* Runs once after component is initialized
* Best place to fetch API data

```ts
ngOnInit() {
  console.log('Component Initialized');
}
```

Use case:
Fetching user data from backend.

---

### 3️⃣ ngOnChanges()

* Runs when @Input() properties change
* Useful in parent-child communication

```ts
@Input() name!: string;

ngOnChanges(changes: any) {
  console.log('Input changed', changes);
}
```

Use case:
When parent sends updated data to child component.

---

### 4️⃣ ngDoCheck()

* Runs during every change detection cycle
* Used for custom change detection
* Rarely needed

```ts
ngDoCheck() {
  console.log('Change detected');
}
```

---

### 5️⃣ ngAfterViewInit()

* Runs after component view (HTML) is initialized
* Used when accessing DOM elements

```ts
ngAfterViewInit() {
  console.log('View Initialized');
}
```

Use case:
Accessing @ViewChild elements.

---

### 6️⃣ ngOnDestroy()

* Runs before component is destroyed
* Used to clean up memory

```ts
ngOnDestroy() {
  console.log('Component Destroyed');
}
```

Use case:

* Unsubscribe from Observables
* Clear timers
* Avoid memory leaks

---

## 5. Real-World Example

Imagine a User Dashboard:

* constructor() → inject services
* ngOnInit() → fetch user data
* ngOnChanges() → update when parent sends new user
* ngAfterViewInit() → load chart after DOM ready
* ngOnDestroy() → unsubscribe from real-time updates

This is how real applications use lifecycle hooks.

---

## 6. Interview Questions & Answers

### Q1: What are lifecycle hooks in Angular?

Answer:
Lifecycle hooks are predefined methods that Angular calls at specific stages of a component’s life.

---

### Q2: Difference between constructor and ngOnInit?

Answer:

* constructor is used for dependency injection.
* ngOnInit is used for initialization logic like API calls.

---

### Q3: When is ngOnChanges called?

Answer:
It is called whenever an @Input() property value changes.

---

### Q4: Which hook is used to clean up subscriptions?

Answer:
ngOnDestroy is used to unsubscribe and prevent memory leaks.

---

### Q5: What is the order of lifecycle hooks?

Answer:
constructor → ngOnChanges → ngOnInit → ngDoCheck → ngAfterContentInit → ngAfterContentChecked → ngAfterViewInit → ngAfterViewChecked → ngOnDestroy

---

### Q6: Why is ngAfterViewInit important?

Answer:
Because DOM elements are available only after view initialization.

---

## 7. Common Mistakes to Avoid

* Calling APIs inside constructor
* Forgetting to unsubscribe in ngOnDestroy
* Overusing ngDoCheck (performance issue)

---

## 8. Key Takeaways

* Lifecycle hooks control component behavior at each stage.
* ngOnInit is most commonly used.
* ngOnDestroy prevents memory leaks.
* Use only necessary hooks.

---

If you are preparing for interviews:

Make sure you can:

* Explain lifecycle in simple terms
* Tell execution order confidently
* Give real project examples
* Explain constructor vs ngOnInit clearly

That clarity makes a strong impression in frontend interviews.
