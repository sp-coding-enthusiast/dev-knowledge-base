# ASP.NET Core – Model Binding & Validation

## 1. What is Model Binding? (Layman Explanation)

**Model Binding** is ASP.NET Core's way of **automatically taking data from an HTTP request** (URL, query string, form, JSON body, headers) and **putting it into your C# objects**.

👉 Think of it like a **translator**:

* User sends data from browser / Postman
* ASP.NET Core reads it
* Converts it into C# method parameters or models

You don’t manually parse request data — **ASP.NET Core does it for you**.

---

## 2. Real-Life Analogy

Imagine a **restaurant order**:

* Customer fills an order slip (request)
* Waiter reads it
* Kitchen gets a clean, structured order ticket (C# object)

Model Binding = the waiter.

---

## 3. Where Does Model Binding Get Data From?

ASP.NET Core checks data **in this order**:

1. Route values (`/users/5`)
2. Query string (`?page=2`)
3. Form data
4. Request body (JSON)
5. Headers (if specified)

---

## 4. Simple Example – Query String Binding

### Request

```
GET /products?category=Books&price=500
```

### Controller

```csharp
public IActionResult GetProducts(string category, int price)
{
    // category = "Books"
    // price = 500
    return Ok();
}
```

✔ No parsing code required

---

## 5. Model Binding with Complex Objects

### Model

```csharp
public class User
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

### Request (JSON)

```json
{
  "name": "Saurabh",
  "age": 30
}
```

### Controller

```csharp
[HttpPost]
public IActionResult CreateUser(User user)
{
    // user.Name = "Saurabh"
    // user.Age = 30
    return Ok(user);
}
```

✔ JSON → C# object automatically

---

## 6. What is Model Validation? (Layman Explanation)

**Model Validation** ensures the data received is:

* Complete
* Correct
* Safe to use

👉 Think of it like **checking the order before cooking**:

* Missing item?
* Invalid quantity?
* Wrong format?

---

## 7. Why Validation Is Important

Without validation:

* App crashes
* Bad data goes to DB
* Security risks

Validation protects your application.

---

## 8. Validation Using Data Annotations

### Model with Validation Rules

```csharp
using System.ComponentModel.DataAnnotations;

public class User
{
    [Required]
    public string Name { get; set; }

    [Range(18, 60)]
    public int Age { get; set; }

    [EmailAddress]
    public string Email { get; set; }
}
```

---

## 9. How Validation Works Internally

1. Model Binding happens first
2. Validation rules are applied
3. Errors are stored in `ModelState`

---

## 10. Checking Validation in Controller

```csharp
[HttpPost]
public IActionResult Register(User user)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }

    return Ok("User registered");
}
```

---

## 11. Automatic Validation in `[ApiController]`

```csharp
[ApiController]
[Route("api/users")]
public class UsersController : ControllerBase
{
    [HttpPost]
    public IActionResult Create(User user)
    {
        return Ok(user);
    }
}
```

✔ ASP.NET Core automatically returns **400 Bad Request** if validation fails
✔ No need to check `ModelState.IsValid`

---

## 12. Common Validation Attributes

| Attribute             | Purpose               |
| --------------------- | --------------------- |
| `[Required]`          | Field must have value |
| `[StringLength]`      | Min / max length      |
| `[Range]`             | Numeric limits        |
| `[EmailAddress]`      | Valid email           |
| `[RegularExpression]` | Pattern match         |

---

## 13. Custom Validation Example

```csharp
public class AdultOnlyAttribute : ValidationAttribute
{
    public override bool IsValid(object value)
    {
        if (value is int age)
            return age >= 18;

        return false;
    }
}
```

```csharp
public class User
{
    [AdultOnly]
    public int Age { get; set; }
}
```

---

## 14. Model Binding vs Validation (Interview Favorite)

| Feature         | Model Binding        | Model Validation   |
| --------------- | -------------------- | ------------------ |
| Purpose         | Map request → object | Verify correctness |
| Happens first   | ✔ Yes                | ❌ No               |
| Uses attributes | ❌ No                 | ✔ Yes              |
| Stores errors   | ❌ No                 | ✔ ModelState       |

---

## 15. Common Interview Questions & Answers

### Q1. What is model binding in ASP.NET Core?

**Answer:**
Model binding automatically maps HTTP request data to action method parameters or model objects.

---

### Q2. Difference between Model Binding and Model Validation?

**Answer:**
Model binding creates objects from request data, while validation ensures the data is valid and safe.

---

### Q3. What is `ModelState`?

**Answer:**
`ModelState` holds validation errors generated during model validation.

---

### Q4. What happens if validation fails in `[ApiController]`?

**Answer:**
ASP.NET Core automatically returns 400 Bad Request with validation errors.

---

### Q5. Can model binding fail?

**Answer:**
Yes, if data types don’t match or required values are missing.

---

## 16. Key Takeaways

* Model Binding = **data mapping**
* Validation = **data checking**
* `[ApiController]` simplifies validation
* Data annotations are most common
* Always validate user input

---

✅ **Interview Tip:**
Say: *"Model binding maps data, validation protects the system."*
