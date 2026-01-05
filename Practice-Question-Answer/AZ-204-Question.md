## Question 1

You are developing an Azure Service application that processes queue data when it receives a message from a mobile application. Messages may not be sent to the service consistently.

You have the following requirements:

- Queue size must not grow larger than **80 GB**
- Use **first-in-first-out (FIFO)** ordering of messages
- **Minimize Azure costs**

You need to implement the messaging solution.

**Proposed Solution:**

- Use the **.NET API** to add a message to an **Azure Storage Queue** from the mobile application  
- Create an **Azure Function App** that uses an **Azure Storage Queue trigger**

**Does the solution meet the goal?**

### OPTIONS
- **A. Yes**
- **B. No**

---

## ✅ Correct Answer

**B. No**

---

## Explanation

Although the proposed solution is inexpensive and commonly used, it does **not fully meet the stated requirements**.

### 1. FIFO Ordering ❌
Azure **Storage Queues do not guarantee strict FIFO ordering**.  
While messages are *generally* dequeued in order, Microsoft explicitly states that ordering is **best-effort only** and **not guaranteed**, especially under high load or with multiple consumers.

> If strict FIFO ordering is required, **Azure Service Bus queues with sessions** are the recommended solution.

---

### 2. Queue Size Limit (80 GB) ❌
Azure Storage Queues:
- Do **not provide a built-in mechanism** to enforce a maximum queue size
- Can grow extremely large (up to hundreds of terabytes per storage account)

Therefore, you **cannot guarantee** the queue will remain under **80 GB** without custom monitoring and cleanup logic, which violates the requirement.

---

### 3. Cost Minimization ✅
Azure Storage Queues **are cheaper** than Azure Service Bus, so this requirement *is* met.

---

## Final Verdict

Because the solution:
- ❌ Does **not guarantee FIFO ordering**
- ❌ Does **not enforce an 80 GB queue size limit**

…it **fails to meet the overall goal**, even though it is cost-effective.

---

### 💡 Recommended Alternative (for completeness)

To meet **all** requirements:
- Use **Azure Service Bus Queue with Sessions**  
  - Guarantees FIFO ordering
  - Allows better control over message retention and size
- Configure **message TTL and monitoring** to control queue growth

This may cost slightly more but satisfies all functional requirements.

---
