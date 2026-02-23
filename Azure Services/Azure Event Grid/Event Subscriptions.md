# Azure Event Subscriptions (Event Grid)

## TL;DR (Simple Idea)

An **event subscription** tells Event Grid **where to send events** when something happens.

Think:

* Event = something happened
* Topic = where events are published
* **Subscription = who should receive it**

Analogy:
You subscribe to a YouTube channel → you get notified when a video is uploaded.

---

# 1. What is an Event Subscription?

In Azure Event Grid, an **event subscription** connects:

Event Source → Event Grid Topic → Event Subscription → Event Handler

It defines:

* Which events to listen to
* Where to send them
* Optional filters

So when an event occurs, Event Grid pushes it to the subscribed endpoint.

---

# 2. Components Explained Simply

## Event Source

Where event originates
Examples:

* Blob Storage
* Resource Group
* Custom App
* IoT service

## Topic

Channel that receives events
Types:

* System topic (Azure services)
* Custom topic (your apps)

## Event Subscription

Rules for delivery
Defines:

* Destination endpoint
* Event types
* Filters

## Event Handler (Subscriber)

Receiver of event
Examples:

* Azure Function
* Logic App
* Webhook
* Service Bus

---

# 3. How It Works (Flow)

Example: File uploaded to storage

Blob Storage → Topic → Subscription → Azure Function

Steps:

1. File uploaded
2. Storage publishes event
3. Event Grid checks subscriptions
4. Matching subscription found
5. Event delivered to Function

---

# 4. Real‑World Examples

## Example 1 — Image Processing

When image uploaded → resize automatically

Subscription:

* Source: Blob Storage
* Event: BlobCreated
* Handler: Azure Function

---

## Example 2 — Order Notification

When order created → send email

Subscription:

* Source: Custom topic
* Event: OrderCreated
* Handler: Logic App

---

## Example 3 — Security Monitoring

When VM deleted → alert team

Subscription:

* Source: Azure Resources
* Event: ResourceDeleteSuccess
* Handler: Webhook

---

# 5. Types of Event Subscriptions

## System Topic Subscription

Events from Azure services
Example: Storage → Function

## Custom Topic Subscription

Events from your app
Example: Ecommerce app → Logic App

## Domain Subscription

Multi‑tenant/event domain routing
Example: SaaS platform customers

---

# 6. Filtering (Important Feature)

Subscriptions can filter events so only relevant ones are delivered.

## By Event Type

Only BlobCreated

## By Subject Prefix/Suffix

Only images/*.jpg

## Advanced Filters

Example:

* Size > 1MB
* Region = US

This prevents unnecessary triggers.

---

# 7. Retry & Delivery Behavior

Event Grid guarantees delivery with retries.

Behavior:

* Push via HTTPS
* Retry for ~24 hours
* Exponential backoff
* Dead‑letter optional

So subscriptions are reliable.

---

# 8. Multiple Subscribers (Fan‑out)

One event → many subscriptions

BlobCreated →

* Function
* Logic App
* Webhook

Each subscription gets its own copy.

---

# 9. Architecture Example

E‑commerce upload pipeline:

User Upload → Storage → Event Grid Topic

Subscriptions:

* Resize Function
* Virus Scan Function
* Metadata Extractor

All triggered independently.

---

# 10. Interview‑Ready Answers

## Q: What is an Event Subscription in Azure Event Grid?

**Answer:**
An event subscription defines the routing rule that tells Event Grid where to deliver events from a topic. It specifies the destination endpoint, event types, and optional filters, enabling event‑driven communication between publishers and subscribers.

---

## Q: What does an event subscription contain?

**Answer:**
It contains the event source/topic, destination endpoint (handler), event type filters, subject filters, and delivery configuration such as retries or dead‑letter settings.

---

## Q: How does filtering help in subscriptions?

**Answer:**
Filtering ensures only relevant events are delivered to a subscriber, reducing unnecessary processing and improving efficiency in event‑driven architectures.

---

## Q: Can multiple subscriptions exist for one topic?

**Answer:**
Yes. Event Grid supports fan‑out, allowing multiple subscriptions on the same topic so different services can independently react to the same event.

---

## Q: Difference between topic and subscription?

**Answer:**
A topic is where events are published, while a subscription defines where those events should be delivered and under what conditions.

---

# 11. Common Azure Handlers

Supported endpoints:

* Azure Function
* Logic App
* Webhook (HTTP)
* Service Bus Queue
* Event Hub
* Storage Queue

---

# 12. When to Use Event Subscriptions

Use when you need:

* Event‑driven automation
* Reactive workflows
* Resource change triggers
* Serverless integration

---

# 13. Memory Trick

Topic = channel
Subscription = listener
Handler = receiver

Or:
No subscription → no delivery

---

# 14. One‑Line Summary

An Event Subscription tells Event Grid which events to send and where to send them.
