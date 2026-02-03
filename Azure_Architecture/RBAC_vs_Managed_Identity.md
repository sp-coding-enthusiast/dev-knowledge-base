# RBAC vs Managed Identity (Azure) – Layman Guide

## 1. Big Picture (Very Simple)

People often confuse **RBAC** and **Managed Identity**, but they solve **different problems**.

* **RBAC** → *WHO can do WHAT on Azure resources*
* **Managed Identity** → *HOW an app proves its identity without passwords*

### One-Line Analogy

* **Managed Identity** = *ID card*
* **RBAC** = *Access permissions written on that ID card*

You almost always use them **together**.

---

## 2. What is RBAC (Role-Based Access Control)?

### Layman Explanation

RBAC decides **who is allowed to do what**.

Like in an office:

* Employee → can read files
* Manager → can edit files
* Admin → can delete files

---

### Azure Definition

**RBAC** is an authorization system that assigns **roles** to identities at a **scope**.

### Example Roles

* Reader → View only
* Contributor → Create/update resources
* Owner → Full control

---

### RBAC Example (Simple)

User: *App1*

* Role: **Reader**
* Resource: Storage Account

Result:

* App1 can **read data**
* App1 **cannot delete** the storage

---

### RBAC Key Concepts

| Concept  | Meaning                                  |
| -------- | ---------------------------------------- |
| Identity | User / App / Service                     |
| Role     | Set of permissions                       |
| Scope    | Subscription / Resource Group / Resource |

---

### RBAC Interview Answer

> RBAC controls access to Azure resources by assigning roles with specific permissions at defined scopes.

---

## 3. What is Managed Identity?

### Layman Explanation

Managed Identity lets an **application log in to Azure automatically** without storing:

* Username
* Password
* Secrets

Azure manages the identity for you.

---

### Simple Analogy

Instead of writing your password on paper and giving it to someone:

* Azure gives the app a **secure badge**
* Azure verifies the badge automatically

---

### Types of Managed Identity

| Type            | Explanation                               |
| --------------- | ----------------------------------------- |
| System-assigned | Identity tied to one resource             |
| User-assigned   | Reusable identity shared across resources |

---

### Managed Identity Example

Scenario:

* Web App needs to read secrets from Key Vault

Without Managed Identity ❌

* Store secret in config (unsafe)

With Managed Identity ✅

* App authenticates automatically
* No credentials stored

---

### Managed Identity Interview Answer

> Managed Identity provides an automatically managed identity for Azure resources to authenticate securely without credentials.

---

## 4. RBAC vs Managed Identity (Side-by-Side)

| Feature        | RBAC                   | Managed Identity         |
| -------------- | ---------------------- | ------------------------ |
| Purpose        | Authorization          | Authentication           |
| Solves         | What access is allowed | How identity is provided |
| Uses roles     | Yes                    | No                       |
| Stores secrets | No                     | No                       |
| Used alone     | Yes                    | No (needs RBAC)          |

---

## 5. How They Work Together (Most Important Part)

### Real-World Azure Flow

1. App uses **Managed Identity** to authenticate
2. Azure verifies the identity
3. **RBAC** checks what the identity is allowed to do
4. Access is granted or denied

### Visual Analogy

* Managed Identity → *Who are you?*
* RBAC → *What are you allowed to do?*

---

## 6. End-to-End Example (Interview Favorite)

### Scenario: Web App reads data from Storage Account

**Step 1:** Enable Managed Identity on Web App

**Step 2:** Assign RBAC Role

* Role: Storage Blob Data Reader
* Scope: Storage Account

**Result:**

* App logs in securely
* App reads blobs
* No secrets stored

---

## 7. When to Use What?

### Use RBAC When:

* You need to control access
* You manage permissions

### Use Managed Identity When:

* App-to-Azure communication
* You want to avoid secrets

### Use Both When:

* Azure services talk to each other (most cases)

---

## 8. Common Interview Questions

### Q1. Can Managed Identity replace RBAC?

**Answer:**
No. Managed Identity handles authentication, while RBAC handles authorization.

---

### Q2. Can RBAC work without Managed Identity?

**Answer:**
Yes, RBAC can be used with users, groups, or service principals.

---

### Q3. Is Managed Identity more secure than service principals?

**Answer:**
Yes, because credentials are fully managed by Azure and not exposed.

---

### Q4. System-assigned vs User-assigned Managed Identity?

**Answer:**
System-assigned is tied to one resource. User-assigned is reusable across resources.

---

## 9. Common Mistakes (Interview Gold)

* Storing secrets in appsettings ❌
* Giving Contributor role when Reader is enough ❌
* Mixing authentication and authorization concepts ❌

---

## 10. One-Line Interview Summary

> Managed Identity provides secure authentication for Azure resources, while RBAC controls what those identities are allowed to do.
