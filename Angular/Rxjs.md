# Angular – RxJS Basics (Layman Explanation + Examples + Interview Q&A)

## 1. What is RxJS? (Simple Explanation)

RxJS stands for Reactive Extensions for JavaScript.

In simple words:

RxJS helps you handle asynchronous data like API calls, user input, timers, and real-time updates in a clean and powerful way.

---

## 2. Simple Analogy

Imagine a water pipe:

* Water flowing inside pipe = Data
* Pipe = Observable
* You watching the water = Subscription

Whenever new water (data) flows, you receive it.

That is exactly how RxJS works.

---

## 3. Why Angular Uses RxJS

Angular heavily uses RxJS for:

* HTTP requests
* Form value changes
* Routing events
* Real-time updates

Example:

When you call an API using HttpClient, Angular returns an Observable.

---

## 4. Core Concepts of RxJS

### 1️⃣ Observable

An Observable is a stream of data that can emit multiple values over time.

Example:

```ts
import { Observable } from 'rxjs';

const observable = new Observable(observer => {
  observer.next('Hello');
  observer.next('World');
  observer.complete();
});
```

---

### 2️⃣ Observer

Observer listens to data emitted by Observable.

```ts
observable.subscribe({
  next: value => console.log(value),
  error: err => console.log(err),
  complete: () => console.log('Completed')
});
```

---

### 3️⃣ Subscription

Subscription is the execution of Observable.

If you do not subscribe, nothing happens.

```ts
const subscription = observable.subscribe(value => console.log(value));
```

---

### 4️⃣ Operators

Operators modify or transform data inside stream.

Common operators:

* map
* filter
* tap
* switchMap
* mergeMap
* debounceTime

Example:

```ts
import { of } from 'rxjs';
import { map } from 'rxjs/operators';

of(1, 2, 3)
  .pipe(
    map(value => value * 2)
  )
  .subscribe(result => console.log(result));
```

Output:
2, 4, 6

---

## 5. Real Angular Example – HTTP Call

```ts
this.http.get('https://api.example.com/users')
  .subscribe(data => {
    console.log(data);
  });
```

What happens?

1. API request is sent
2. Response comes later
3. Observable emits response
4. subscribe() receives it

---

## 6. Important RxJS Operators Explained Simply

### map()

Transforms data.

### filter()

Filters values.

### tap()

Used for debugging or side effects.

### switchMap()

Cancels previous request and switches to new one.
Used in search boxes.

### debounceTime()

Waits for some time before emitting value.
Used in search input.

Example – Search Box Optimization:

```ts
searchControl.valueChanges
  .pipe(
    debounceTime(300),
    switchMap(value => this.http.get('api/search?q=' + value))
  )
  .subscribe(result => console.log(result));
```

---

## 7. Observable vs Promise

| Observable         | Promise              |
| ------------------ | -------------------- |
| Multiple values    | Single value         |
| Can be cancelled   | Cannot cancel        |
| Lazy execution     | Executes immediately |
| Powerful operators | Limited              |

---

## 8. Memory Leak Prevention

If you subscribe manually, always unsubscribe.

```ts
subscription.unsubscribe();
```

Or use:

* async pipe
* takeUntil
* take(1)

Example:

```ts
ngOnDestroy() {
  this.subscription.unsubscribe();
}
```

---

## 9. Interview Questions & Answers

### Q1: What is RxJS?

Answer:
RxJS is a library for handling asynchronous data using Observables.

---

### Q2: What is an Observable?

Answer:
An Observable is a stream of data that emits values over time.

---

### Q3: Difference between Observable and Promise?

Answer:
Observable can emit multiple values and can be cancelled, whereas Promise emits one value and cannot be cancelled.

---

### Q4: What is switchMap used for?

Answer:
It switches to a new Observable and cancels the previous one. Commonly used in search API calls.

---

### Q5: What causes memory leaks in RxJS?

Answer:
Not unsubscribing from Observables when component is destroyed.

---

### Q6: What is async pipe?

Answer:
Async pipe automatically subscribes and unsubscribes from Observables in template.

Example:

```html
<p>{{ user$ | async }}</p>
```

---

## 10. Real-World Example

Imagine a live stock market app:

* Prices update every second
* Data stream keeps emitting values
* Observable handles continuous updates
* Component unsubscribes when user leaves page

That is RxJS in action.

---

## 11. Key Takeaways

* RxJS handles asynchronous streams.
* Observable is core concept.
* Operators transform data.
* switchMap is important for APIs.
* Always prevent memory leaks.

---

If preparing for interviews, be able to:

* Explain Observable clearly
* Explain map vs switchMap
* Explain Observable vs Promise
* Give real project example

Strong RxJS knowledge separates average Angular developers from advanced ones.
