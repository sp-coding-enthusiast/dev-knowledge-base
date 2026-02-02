# ASP.NET Core – JWT Authentication Internals

## 1. What is JWT? (Layman Explanation)

**JWT** stands for **JSON Web Token**.

In simple words:
👉 JWT is a **digital ID card** that proves *who you are* when calling an API.

Once you log in successfully:

* Server gives you a **token**
* You send this token with every request
* Server trusts the token instead of asking for username/password again

---

## 2. Real-Life Analogy

Think of **office access card**:

* You show ID once (login)
* You get an access card (JWT)
* Every door checks the card
* No need to show ID again

JWT works exactly like this.

---

## 3. Why JWT is Needed

Without JWT:

* Username/password sent every time ❌
* Server sessions required ❌

With JWT:

* Stateless authentication ✔
* Scales well ✔
* Works across devices ✔

---

## 4. What Does a JWT Look Like?

A JWT has **three parts**, separated by dots:

```
xxxxx.yyyyy.zzzzz
```

### 1️⃣ Header

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### 2️⃣ Payload (Claims)

```json
{
  "sub": "123",
  "name": "Saurabh",
  "role": "Admin",
  "exp": 1710000000
}
```

### 3️⃣ Signature

Used to **verify token is not tampered**.

---

## 5. Important Rule (Interview Critical)

⚠ JWT is **Base64 encoded, NOT encrypted**.

Anyone can read payload.
❌ Do not store passwords or secrets.

---

## 6. JWT Authentication Flow (Step-by-Step)

1. Client sends username/password
2. Server validates credentials
3. Server creates JWT
4. JWT sent to client
5. Client stores JWT
6. Client sends JWT in every request
7. Server validates JWT
8. Access granted

---

## 7. How JWT is Sent to API

JWT is sent in **Authorization header**:

```
Authorization: Bearer <token>
```

---

## 8. JWT Internals in ASP.NET Core

ASP.NET Core uses **middleware** to validate JWT **before controller executes**.

Pipeline order:

```
Request → Authentication Middleware → Authorization → Controller
```

---

## 9. JWT Configuration in ASP.NET Core

```csharp
builder.Services.AddAuthentication("Bearer")
    .AddJwtBearer(options =>
    {
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            ValidateIssuerSigningKey = true,
            ValidIssuer = "myapp",
            ValidAudience = "myapp",
            IssuerSigningKey = new SymmetricSecurityKey(
                Encoding.UTF8.GetBytes("SuperSecretKey"))
        };
    });
```

---

## 10. What Happens Internally (Deep but Simple)

When request comes:

1. Middleware extracts token
2. Signature is verified
3. Expiry is checked
4. Issuer & audience validated
5. Claims are loaded into `HttpContext.User`

If anything fails → **401 Unauthorized**

---

## 11. Claims Explained Simply

**Claims** are pieces of information about user.

Examples:

* UserId
* Role
* Email

```csharp
User.FindFirst("role")
```

---

## 12. Authorization Using JWT

```csharp
[Authorize]
public IActionResult GetData() => Ok();

[Authorize(Roles = "Admin")]
public IActionResult AdminOnly() => Ok();
```

---

## 13. Token Expiration & Refresh Tokens

JWT expires for security.

* Access Token → short life
* Refresh Token → long life

Refresh token is used to get new JWT.

---

## 14. Stateless Authentication (Big Interview Point)

JWT authentication is **stateless**:

* Server stores no session
* Token has all info

This makes JWT perfect for:

* Microservices
* Cloud apps

---

## 15. JWT vs Cookies (Interview Comparison)

| JWT              | Cookies           |
| ---------------- | ----------------- |
| Stateless        | Stateful          |
| Stored on client | Stored on browser |
| Scales easily    | Harder to scale   |

---

## 16. Common JWT Security Best Practices

* Use HTTPS always
* Keep token expiry short
* Never store secrets in JWT
* Use strong signing key

---

## 17. Common Interview Questions & Answers

### Q1. What is JWT?

**Answer:**
JWT is a compact token used for stateless authentication between client and server.

---

### Q2. Is JWT encrypted?

**Answer:**
No, JWT is only encoded and signed.

---

### Q3. Where is JWT validated?

**Answer:**
In authentication middleware before controller execution.

---

### Q4. How does JWT maintain statelessness?

**Answer:**
All user data is inside the token, no server session is stored.

---

### Q5. Difference between Authentication and Authorization?

**Answer:**
Authentication verifies identity, authorization verifies access rights.

---

## 18. Common Mistakes

* Storing sensitive data in JWT
* Long token expiry
* Skipping HTTPS

---

## 19. Key Takeaways

* JWT = digital identity
* Stateless & scalable
* Middleware-driven
* Claims-based authorization

---

✅ **Interview One-Liner:**
"JWT provides stateless, scalable authentication by validating signed tokens on every request."
