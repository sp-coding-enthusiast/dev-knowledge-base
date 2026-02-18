# ConfigMaps in Kubernetes – Simple Explanation

## Why Do We Need ConfigMaps? 🤔

We already know **environment variables** are used to pass values to our application.

But imagine this situation 👇

* You have **hundreds of environment variables**
* The **same variables** are needed by:

  * Backend app
  * Frontend app
  * Worker app
* You are **copy-pasting** the same key–value pairs into multiple Kubernetes YAML files

This quickly becomes:

* Hard to manage 😓
* Error‑prone ❌
* Difficult to update 🔄

👉 **ConfigMaps solve this problem.**

---

## What Is a ConfigMap? 🧠

A **ConfigMap** is a **Kubernetes object** used to store **non‑secret configuration data** such as:

* Environment variables
* App configuration values
* URLs
* Feature flags

Instead of writing environment variables inside every deployment, you:

1. Store them **once** in a ConfigMap
2. Reuse them in **multiple deployments**

---

## Layman Analogy 📝

Think of a **ConfigMap** as a **shared notebook**.

* The notebook contains configuration values
* Multiple people (apps) read from the same notebook
* If something changes, you update it **once**, not everywhere

---

## Problem Without ConfigMap ❌

```yaml
env:
- name: APP_MODE
  value: "production"
- name: LOG_LEVEL
  value: "info"
- name: API_URL
  value: "https://api.example.com"
- name: REGION
  value: "us-east-1"
```

Now imagine:

* 100 such variables
* 5 deployments

That’s **500 lines of duplicate config** 😬

---

## Solution With ConfigMap ✅

### Step 1: Create a ConfigMap

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_MODE: "production"
  LOG_LEVEL: "info"
  API_URL: "https://api.example.com"
  REGION: "us-east-1"
```

All configuration is now stored **in one place**.

---

### Step 2: Use ConfigMap in a Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-app
spec:
  replicas: 1
  template:
    spec:
      containers:
      - name: app
        image: my-app
        envFrom:
        - configMapRef:
            name: app-config
```

🎯 Result:

* All values from `app-config` become environment variables
* No duplication

---

### Step 3: Reuse the Same ConfigMap

```yaml
envFrom:
- configMapRef:
    name: app-config
```

You can use this in:

* Frontend deployment
* Backend deployment
* Worker deployment

One ConfigMap → Many apps

---

## How Applications Use ConfigMaps 🧩

Once injected:

* Variables are available inside the **container**
* Application code reads them like normal env variables

Example (Python):

```python
import os
print(os.getenv("API_URL"))
```

---

## How to Create ConfigMaps 📦

### 1️⃣ Declarative Way (Recommended)

* Write YAML
* Apply using `kubectl apply`
* Version controlled

### 2️⃣ Imperative Way

```bash
kubectl create configmap app-config \
  --from-literal=APP_MODE=production
```

Useful for quick testing

---

## What Should Go Into ConfigMaps? ✅

✔ Allowed:

* App configuration
* URLs
* Feature flags
* Environment-specific values

❌ Not Allowed:

* Passwords
* Tokens
* API keys

👉 Use **Secrets** for sensitive data

---

## ConfigMap vs Environment Variables 🆚

| Feature                | Env Variables       | ConfigMap   |
| ---------------------- | ------------------- | ----------- |
| Management             | Manual & repetitive | Centralized |
| Reusability            | Poor                | Excellent   |
| Kubernetes-native      | No                  | Yes         |
| Best for large configs | ❌                   | ✅           |

---

## Common Interview Questions & Answers 🎯

### 1. What is a ConfigMap?

**Answer:**
A ConfigMap is a Kubernetes object used to store non-sensitive configuration data that can be injected into containers as environment variables or files.

---

### 2. Why use ConfigMaps instead of plain environment variables?

**Answer:**
ConfigMaps provide centralized management, reduce duplication, and make configuration reusable across multiple deployments.

---

### 3. Can a ConfigMap be used by multiple pods?

**Answer:**
Yes. A single ConfigMap can be referenced by multiple pods and deployments.

---

### 4. Are ConfigMaps secure?

**Answer:**
No. ConfigMaps are not encrypted. Sensitive data should be stored in Kubernetes Secrets.

---

### 5. How can ConfigMap values be consumed by a pod?

**Answer:**
They can be consumed as environment variables or mounted as files inside the container.

---

### 6. What happens if a ConfigMap is updated?

**Answer:**
Existing pods do not automatically restart. Pods must be restarted to pick up updated values (unless mounted as volumes with reload logic).

---

### 7. What is the difference between ConfigMap and Secret?

**Answer:**
ConfigMaps store non-sensitive data in plain text, while Secrets store sensitive data in base64-encoded format.

---

## Key Takeaways ✅

* ConfigMaps are an **advanced and Kubernetes-native way** to manage environment variables
* They avoid duplication across manifests
* One ConfigMap can serve multiple applications
* Perfect for non-secret configuration data

---

📌 **Next Topic:**
Secrets – secure way to manage passwords and credentials
