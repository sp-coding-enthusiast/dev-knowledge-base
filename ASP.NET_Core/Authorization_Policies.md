# ASP.NET Core – Authorization Policies

## 1. What is Authorization? (Layman Explanation)

**Authorization** answers one simple question:
👉 *Are you allowed to do this?*

* Authentication = Who are you?
* Authorization = What are you allowed to do?

Authorization **always comes after authentication**.

---

## 2. Real-Life Analogy

Think of an **office building**:

* Security checks your ID → Authentication
* Access card decides which floors you can enter → Authorization

Authorization policies are the **rules on the access card**.

---

## 3. What are Authorization Policies?

An **authorization policy** is a **named set of rules** that decides whether a user can access a resource.

In simple terms:
👉 Policy = *Condition(s) that must be true to allow access*

---

## 4. Why Authorization Policies Are Needed

Without policies:

* Hard-coded role checks everywhere ❌
* Duplicate logic ❌

With policies:

* Centralized rules ✔
* Clean controllers ✔
* Easy to change ✔

---

## 5. Role-Based Authorization (Basic)

```csharp
[Authorize(Roles = "Admin")]
public IActionResult DeleteUser() => Ok();
```

✔ Simple
❌ Not flexible

---

## 6. Policy-Based Authorization (Recommended)

Policies allow **complex conditions**:

* Role
* Claims
* Custom logic

---

## 7. Defining Authorization Policies

```csharp
builder.Services.AddAuthorization(options =>
{
    options.AddPolicy("AdminOnly", policy =>
        policy.RequireRole("Admin"));

    options.AddPolicy("AdultUser", policy =>
        policy.RequireClaim("Age", "18"));
});
```

---

## 8. Using Policies in Controllers

```csharp
[Authorize(Policy = "AdminOnly")]
public IActionResult GetSecretData() => Ok();
```

---

## 9. Policy with Multiple Requirements

```csharp
options.AddPolicy("AdminManager", policy =>
{
    policy.RequireRole("Admin");
    policy.RequireClaim("Department", "IT");
});
```

✔ All conditions must be satisfied

---

## 10. Claims-Based Authorization (Layman View)

**Claims** are facts about a user.

Examples:

* Role = Admin
* Country = India
* Age = 30

Policies check these facts.

---

## 11. Custom Authorization Requirement

### Step 1: Create Requirement

```csharp
public class MinimumAgeRequirement : IAuthorizationRequirement
{
    public int Age { get; }
    public MinimumAgeRequirement(int age)
    {
        Age = age;
    }
}
```

---

### Step 2: Create Handler

```csharp
public class MinimumAgeHandler : AuthorizationHandler<MinimumAgeRequirement>
{
    protected override Task HandleRequirementAsync(
        AuthorizationHandlerContext context,
        MinimumAgeRequirement requirement)
    {
        var ageClaim = context.User.FindFirst("Age");

        if (ageClaim != null && int.Parse(ageClaim.Value) >= requirement.Age)
        {
            context.Succeed(requirement);
        }

        return Task.CompletedTask;
    }
}
```

---

### Step 3: Register Policy

```csharp
options.AddPolicy("AtLeast18", policy =>
    policy.Requirements.Add(new MinimumAgeRequirement(18)));
```

---

## 12. Register Authorization Handler

```csharp
builder.Services.AddSingleton<IAuthorizationHandler, MinimumAgeHandler>();
```

---

## 13. Applying Policy at Controller or Action Level

```csharp
[Authorize(Policy = "AtLeast18")]
public IActionResult BuyProduct() => Ok();
```

---

## 14. Authorization Flow (Internals)

1. User is authenticated
2. Policy is evaluated
3. Requirements are checked
4. Handler succeeds or fails

Fail → **403 Forbidden**

---

## 15. Authorization Policies vs Roles (Interview Favorite)

| Roles        | Policies    |
| ------------ | ----------- |
| Simple       | Flexible    |
| Hard-coded   | Centralized |
| Not scalable | Scalable    |

---

## 16. Common Interview Questions & Answers

### Q1. What is an authorization policy?

**Answer:**
A named set of rules that determines whether a user can access a resource.

---

### Q2. Difference between authentication and authorization?

**Answer:**
Authentication verifies identity, authorization verifies permissions.

---

### Q3. When do policies run?

**Answer:**
After authentication and before controller execution.

---

### Q4. Can policies use custom logic?

**Answer:**
Yes, using custom requirements and handlers.

---

### Q5. What status code is returned if authorization fails?

**Answer:**
403 Forbidden.

---

## 17. Common Mistakes

* Mixing authentication & authorization
* Overusing roles
* Not centralizing rules

---

## 18. Key Takeaways

* Authorization controls access
* Policies are flexible & clean
* Claims enable fine-grained control
* Custom handlers handle complex rules

---

✅ **Interview One-Liner:**
"Authorization policies define centralized, rule-based access control evaluated after authentication."
