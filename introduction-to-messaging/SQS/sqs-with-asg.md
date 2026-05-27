
### **Resume: SQS + Auto Scaling Group (ASG)**

This is the "Elastic Buffer" pattern. Use this when you have a **Producer** (User/App) that is faster than your **Consumer** (Database/Worker).

1.  **The Metric:** The Back-end ASG scales based on **Queue Depth** (`ApproximateNumberOfMessagesVisible`), **NOT** CPU usage.
2.  **Decoupling:** If the Back-end instances crash, the messages stay safe in SQS for up to 14 days. 
3.  **Smoothing Spikes:** SQS "absorbs" the pressure. Even if 1 million users hit the front-end, the back-end continues to work at its own pace without crashing the database.
4.  **Visibility Timeout:** The "Hidden Period." Ensure this is **longer** than your processing time to prevent duplicate work.
5.  **Cost Efficiency:** You can set the Back-end ASG to **Scale to Zero** if the queue is empty.

**Exam Trigger:** "Handle unpredictable traffic spikes while protecting a downstream database." → **SQS + ASG.**

---

### **Moving to SNS: Simple Notification Service**

If SQS is a **"Private Inbox"** (one person pulls one message), **SNS** is a **"Global Broadcaster"** (one message is pushed to many people).

#### **1. The Core Concept (Pub/Sub)**
*   **Publishers:** Send a message to an **SNS Topic**.
*   **Subscribers:** Anyone "listening" to that topic receives the message immediately.
*   **The Model:** **Push** (SNS sends it to you) vs. **Pull** (You check SQS for messages).

#### **2. Who are the Subscribers?**
SNS can send messages to:
*   **SQS Queues** (The most common DevOps pattern).
*   **Lambda Functions** (Triggering code).
*   **HTTP/HTTPS Endpoints** (Webhooks).
*   **Email / SMS / Mobile Push Notifications**.

---

### **3. The "Fan-Out" Pattern (SNS + SQS)**
This is a **guaranteed exam topic**. This is how you send one event to multiple independent systems.

*   **The Scenario:** A user buys a product.
    *   **SNS Topic:** "NewOrder"
    *   **Subscriber 1 (SQS Queue A):** For the "Shipping Department" workers.
    *   **Subscriber 2 (SQS Queue B):** For the "Invoicing Department" workers.
    *   **Subscriber 3 (Email):** To the Customer.
*   **The Benefit:** If the Invoicing system is down, the Shipping system still gets the message. They are **totally independent.**

---

### **DevOps Comparison for your notes:**

| Feature | SQS (Simple Queue Service) | SNS (Simple Notification Service) |
| :--- | :--- | :--- |
| **Delivery** | **Pull** (Workers ask for data). | **Push** (SNS delivers to you). |
| **Persistence** | Messages sit in queue (up to 14 days). | **No persistence.** If no one is subbed, message is lost. |
| **Consumers** | One message = One consumer. | One message = **Many subscribers.** |
| **Analogy** | **The Mailbox** (I check it when I want). | **The Radio** (You have to be tuned in). |

---

