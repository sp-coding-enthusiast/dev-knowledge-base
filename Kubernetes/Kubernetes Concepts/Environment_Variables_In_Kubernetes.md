# Environment Variables in Kubernetes – Simple Explanation

## What is an Environment Variable? 🤔

Think of an **environment variable** as a **labelled note** you stick next to your application.

Instead of hard‑coding values (like usernames, URLs, or configuration settings) inside your code, you keep them **outside** and pass them in when the application runs.

**Real‑life analogy:**

* Your phone = application code
* Your SIM card settings (network name, number) = environment variables
* You can change SIM settings without changing the phone itself

---

## Why Do We Need Environment Variables?

Because:

* We don’t want to change code every time a value changes
* The same app runs in **dev**, **test**, and **prod** with different settings
* Sensitive values (like passwords) should not be inside code

---

## How Environment Variables Work (Simple Flow)

1. You write your **application code**
2. You create a **Kubernetes manifest (YAML file)**
3. You define environment variables in the manifest as **key–value pairs**
4. Kubernetes injects these values into:

   * The **container**
   * The **application running inside the container**

So both the container *and* the app can access them.

---

## Simple Example (Without Kubernetes First)

### Example in a Normal System

Environment Variable:

```
NAME=Piyush
```

Application Code (Python example):

```python
import os
print(os.getenv("NAME"))
```

Output:

```
Piyush
```

You didn’t write `"Piyush"` in code — it came from outside.

---

## Same Idea in Kubernetes 🚢

### Kubernetes Manifest Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: demo-pod
spec:
  containers:
  - name: demo-container
    image: nginx
    env:
    - name: FIRST_NAME
      value: "Piyush"
    - name: LAST_NAME
      value: "Sharma"
```

### What’s Happening Here?

* `FIRST_NAME` and `LAST_NAME` are environment variables
* Kubernetes injects them into the container
* Your application inside the container can read them

---

## Accessing Environment Variables Inside the Container

Once the pod is running, you can check them using:

```bash
env
```

or

```bash
printenv FIRST_NAME
```

Output:

```
Piyush
```

This proves the variable is:

* Available to the container
* Available to the application

---

## Why This Is Powerful 💡

You can:

* Change configuration **without rebuilding images**
* Use the same image in multiple environments
* Control app behavior dynamically

Example use cases:

* Database URLs
* Feature flags
* API endpoints
* Application modes (dev/prod)

---

## Common Interview Questions & Answers 🎯

### 1. What is an environment variable?

**Answer:**
An environment variable is a key–value pair used to pass configuration data to an application at runtime without changing the code.

---

### 2. Why are environment variables important in Kubernetes?

**Answer:**
They allow configuration to be injected into containers dynamically, making applications portable, flexible, and easier to manage across environments.

---

### 3. Where are environment variables defined in Kubernetes?

**Answer:**
They are defined in Kubernetes manifests (YAML files) under the `env` section of a container specification.

---

### 4. Are environment variables available to both the container and the application?

**Answer:**
Yes. Environment variables are available at the container level and can be accessed by the application running inside it.

---

### 5. Can we view environment variables inside a running pod?

**Answer:**
Yes. By logging into the pod and using commands like `env` or `printenv`.

---

### 6. Is it a good idea to store passwords as plain environment variables?

**Answer:**
Not recommended. Kubernetes Secrets should be used instead for sensitive information.

---

### 7. What happens if an environment variable is missing?

**Answer:**
The application may use a default value (if coded) or fail at runtime, depending on how the app handles missing variables.

---

## Key Takeaways ✅

* Environment variables keep configuration **outside code**
* Kubernetes injects them using YAML manifests
* They are accessible to both containers and applications
* They make applications flexible, secure, and production‑ready

---
