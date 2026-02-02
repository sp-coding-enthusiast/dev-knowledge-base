# ASP.NET Core – REST Principles

## 1. What is REST? (Layman Explanation)

**REST** stands for **Representational State Transfer**.

In simple words:
👉 REST is a **set of rules** for building APIs so that **clients and servers can communicate clearly, consistently, and predictably**.

Think of REST like **traffic rules** for APIs.

* If everyone follows them → smooth traffic
* If not → confusion and crashes

---

## 2. Real-Life Analogy

Imagine a **restaurant menu**:

* Menu = API endpoints
* Items = resources (users, orders, products)
* You use standard actions: order, update, cancel

REST says:

* Use **nouns** (items)
* Use **standard actions** (HTTP methods)

---

## 3. What is a Resource?

A **resource** is anything you want to work with.

Examples:

* User
* Product
* Order

In REST, each resource has a **unique URL**.

```
/users
/products
/orders
```

---

## 4. Use Nouns, Not Verbs (Very Important)

❌ Bad REST API:

```
/getUsers
/createUser
/deleteUser
```

✅ Good REST API:

```
GET    /users
POST   /users
DELETE /users/5
```

👉 **HTTP method already tells the action**.

---

## 5. HTTP Methods and Their Meaning

| Method | Meaning        | Example      |
| ------ | -------------- | ------------ |
| GET    | Read data      | Get users    |
| POST   | Create data    | Add new user |
| PUT    | Replace data   | Update user  |
| PATCH  | Partial update | Update email |
| DELETE | Remove data    | Delete user  |

---

## 6. Example – RESTful Users API

### Get all users

```
GET /api/users
```

### Get one user

```
GET /api/users/5
```

### Create user

```
POST /api/users
```

Body:

```json
{ "name": "Saurabh", "age": 30 }
```

### Update user

```
PUT /api/users/5
```

### Delete user

```
DELETE /api/users/5
```

---

## 7. Statelessness (Core REST Rule)

**Stateless** means:
👉 Server does NOT remember previous requests.

Each request must contain:

* Authentication info
* Required data

❌ Bad:

* Server remembers who you are

✅ Good:

* Each request is independent

---

## 8. Why Stateless is Important

* Scales easily
* Easier to debug
* No server-side session dependency

---

## 9. Use Proper HTTP Status Codes

REST APIs must communicate using **status codes**.

| Code | Meaning      | When to use      |
| ---- | ------------ | ---------------- |
| 200  | OK           | Successful GET   |
| 201  | Created      | Resource created |
| 204  | No Content   | Delete success   |
| 400  | Bad Request  | Validation error |
| 401  | Unauthorized | Not logged in    |
| 403  | Forbidden    | No permission    |
| 404  | Not Found    | Resource missing |
| 500  | Server Error | Crash            |

---

## 10. Representations (JSON)

REST does NOT care about UI.
It sends **representations** of data.

Most common: **JSON**

```json
{
  "id": 1,
  "name": "Laptop",
  "price": 50000
}
```

---

## 11. REST in ASP.NET Core (Controller Example)

```csharp
[ApiController]
[Route("api/users")]
public class UsersController : ControllerBase
{
    [HttpGet]
    public IActionResult GetUsers() => Ok();

    [HttpGet("{id}")]
    public IActionResult GetUser(int id) => Ok();

    [HttpPost]
    public IActionResult CreateUser(User user) => Created("/api/users/1", user);

    [HttpPut("{id}")]
    public IActionResult UpdateUser(int id, User user) => NoContent();

    [HttpDelete("{id}")]
    public IActionResult DeleteUser(int id) => NoContent();
}
```

---

## 12. Idempotency (Interview Favorite)

**Idempotent** means:
👉 Calling an API multiple times gives the **same result**.

| Method | Idempotent? |
| ------ | ----------- |
| GET    | ✔ Yes       |
| PUT    | ✔ Yes       |
| DELETE | ✔ Yes       |
| POST   | ❌ No        |

---

## 13. HATEOAS (Optional but REST Concept)

HATEOAS = Hypermedia As The Engine Of Application State

Response contains **links** to next actions.

```json
{
  "id": 1,
  "name": "User",
  "links": {
    "self": "/users/1",
    "delete": "/users/1"
  }
}
```

---

## 14. REST vs RPC (Interview Trap)

| REST           | RPC            |
| -------------- | -------------- |
| Resource-based | Action-based   |
| Uses nouns     | Uses verbs     |
| HTTP semantics | Custom actions |

---

## 15. Common REST Mistakes

* Using verbs in URL
* Ignoring status codes
* Stateful APIs
* Always returning 200

---

## 16. Interview Questions & Answers

### Q1. What is REST?

**Answer:**
REST is an architectural style for designing scalable and stateless APIs using standard HTTP methods.

---

### Q2. Why REST is stateless?

**Answer:**
Statelessness improves scalability, reliability, and simplicity.

---

### Q3. Difference between PUT and PATCH?

**Answer:**
PUT replaces the entire resource, PATCH updates only specific fields.

---

### Q4. Is REST tied to HTTP?

**Answer:**
No, but HTTP is the most common implementation.

---

### Q5. Is REST secure?

**Answer:**
REST itself is not secure; security is added using HTTPS, OAuth, JWT, etc.

---

## 17. Key Takeaways

* REST is about **rules & consistency**
* Resources + HTTP methods
* Stateless communication
* Correct status codes matter
* Easy to test and scale

---

✅ **Interview One-Liner:**
"REST uses standard HTTP methods to operate on resources in a stateless and scalable way."
