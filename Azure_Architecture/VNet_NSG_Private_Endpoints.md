# Azure Architecture: VNET, NSG, Private Endpoints

## 1. Big Picture (Layman View)

Think of Azure like a **large gated city**:

* **VNET (Virtual Network)** = Your **private neighborhood** inside the city
* **NSG (Network Security Group)** = **Security guards + rules** at gates and doors
* **Private Endpoint** = A **private tunnel** to a service, instead of using public roads

These three together control **who can talk to whom, how, and from where**.

---

## 2. Azure VNET (Virtual Network)

### What is it?

A **VNET** is your **own private network** in Azure where you place:

* Virtual Machines
* App Services (with integration)
* Databases (via private endpoints)

It is **isolated by default** from other VNETs and the internet.

### Layman Example

Imagine an **office building**:

* Each company has its **own floor**
* Other companies cannot enter unless allowed

That floor is your **VNET**.

### Key Concepts

* **Address space**: IP range (e.g., 10.0.0.0/16)
* **Subnets**: Rooms inside the floor (e.g., web, app, db)
* **Peering**: Connecting two VNETs like a skywalk

### Simple Example

```text
VNET: 10.0.0.0/16
 ├── Web Subnet: 10.0.1.0/24
 ├── App Subnet: 10.0.2.0/24
 └── DB Subnet : 10.0.3.0/24
```

### Interview Points

* VNET provides **network isolation**
* Supports **hybrid connectivity** (VPN, ExpressRoute)
* VNET peering is **private and high-speed**

---

## 3. NSG (Network Security Group)

### What is it?

An **NSG** is a **rule book** that decides:

* Allow or deny traffic
* Based on IP, port, protocol, direction

It works at:

* **Subnet level** or
* **NIC (VM) level**

### Layman Example

Think of **security guards**:

* One guard at the **building entrance** (subnet NSG)
* One guard at the **office door** (NIC NSG)

Both must allow you in.

### Example Rules

| Rule          | Meaning               |
| ------------- | --------------------- |
| Allow TCP 80  | Allow website traffic |
| Allow TCP 443 | Allow HTTPS           |
| Deny All      | Block everything else |

### Simple NSG Rule Example

```text
Inbound Rules:
- Allow Internet → WebSubnet on port 80
- Allow AppSubnet → DBSubnet on port 1433
- Deny All
```

### Important Behavior

* Rules are processed by **priority number** (lower = higher priority)
* Default rules allow:

  * VNET-to-VNET traffic
  * Azure Load Balancer

### Interview Points

* NSG is **stateful** (response traffic is auto-allowed)
* Always follow **least privilege principle**
* Subnet NSG + NIC NSG = **combined effect**

---

## 4. Private Endpoint

### What is it?

A **Private Endpoint** gives a **private IP** from your VNET to an Azure service like:

* Azure SQL
* Storage Account
* Key Vault

Traffic **never goes to the public internet**.

### Layman Example

Instead of:

* Driving on **public roads** to reach a bank

You get:

* A **private underground tunnel** directly from your office to the bank vault

That tunnel is a **Private Endpoint**.

### Why It Matters

* No public exposure
* Higher security
* Meets compliance requirements

### Example Flow

```text
VM → Private IP (10.0.3.5) → Azure SQL
(No public internet involved)
```

### DNS Is Important

When using private endpoints:

* Public DNS name resolves to **private IP**
* Requires **Private DNS Zone**

Example:

```text
mydb.database.windows.net → 10.0.3.5
```

### Interview Points

* Private Endpoint uses **Azure Private Link**
* Works with PaaS services
* Replaces service endpoints in most secure designs

---

## 5. How They Work Together (Real Scenario)

### Scenario: Secure Web Application

Architecture:

* Web VM in Web Subnet
* App VM in App Subnet
* Azure SQL via Private Endpoint

Flow:

1. Internet → Web VM (allowed by NSG)
2. Web VM → App VM (VNET internal traffic)
3. App VM → Azure SQL (via Private Endpoint)

Security:

* DB has **no public access**
* NSGs block unnecessary ports
* Entire app runs inside VNET

---

## 6. Common Interview Questions & Answers

### Q1: Difference between VNET and Subnet?

**Answer:**
VNET is the container network; subnets are logical divisions inside it.

### Q2: Can NSG be attached to both subnet and NIC?

**Answer:**
Yes. Both apply, and the most restrictive rule wins.

### Q3: Private Endpoint vs Service Endpoint?

**Answer:**

* Service Endpoint: Secures traffic but still uses public endpoint
* Private Endpoint: Uses private IP, no public exposure

### Q4: Is NSG stateless or stateful?

**Answer:**
Stateful — response traffic is automatically allowed.

### Q5: Why use Private Endpoint?

**Answer:**
To securely access PaaS services without exposing them to the internet.

---

## 7. One-Line Summary (For Interviews)

* **VNET**: Private network in Azure
* **NSG**: Traffic control rules
* **Private Endpoint**: Private access to Azure services

Together they form the **foundation of secure Azure architecture**.
