# SNS + SQS: Fan Out 

- Push once in SNS receive in all SQS queues that are subscribers 
- Fully decoupled, no data loss 
- SQS allows for: data persistence, delayed processing and retries of work 
- Ability to add more SQS subscribers over time 
- Make sure your SQS queue access policiy allows for sns to write 
- Cross region Delivery: Works with SQS queues in other regions 

This graphic explains a very common **"Workaround"** for a technical limitation in S3. It is a classic **Fan-out Architecture**.

### **The Problem: The "S3 One-Rule" Limit**
*   **The Constraint:** In Amazon S3, you can only have **one** event rule for a specific combination of event (e.g., `ObjectCreated`) and folder/prefix (e.g., `images/`).
*   **The Conflict:** What if the **Marketing Team** needs to resize the image (via Lambda) AND the **Audit Team** needs to log the upload (via SQS) at the same time? S3 won't let you send that one event to two different places.

---

### **The Solution: SNS Fan-out**
To bypass the limit, you use **SNS as a "Middleman."**

1.  **S3 Config:** You tell S3 to send all "Object Created" events to **one** destination: an **SNS Topic**. (This satisfies the "one-rule" limit).
2.  **The Fan-out:** You "subscribe" multiple services to that SNS Topic. 
3.  **The Result:** When one file is uploaded, SNS **broadcasts** (fans out) the message to:
    *   **SQS Queue A:** (For the Marketing Team).
    *   **SQS Queue B:** (For the Audit Team).
    *   **Lambda Function:** (For immediate processing).

---

### **Exam "Cheat Sheet" for your notes:**

| If the question says... | The Answer is **SNS Fan-out** |
| :--- | :--- |
| **"Send S3 events to multiple destinations"** | **S3 → SNS → SQS/Lambda**. |
| **"Overcome S3 event notification limitations"** | Use **SNS** to fan-out the messages. |
| **"Independent processing of the same S3 event"** | **SNS Fan-out**. |

---

### **SNS FIFO + SQS FIFO**

In standard SNS/SQS, messages can occasionally arrive out of order. In **FIFO**, AWS guarantees that the order in which messages are sent is exactly the order in which they are received.

---

### **The 3 Reasons to use this (From the slide):**

1.  **Ordering:** Messages follow a strict sequence. 
    *   *Example:* 1. Create Account $\rightarrow$ 2. Add Balance $\rightarrow$ 3. Purchase. You cannot do #3 before #1.
2.  **Deduplication:** Prevents the same message from being processed twice. If the "Buying Service" accidentally sends the same "Order ID" two times, SNS FIFO will recognize it and **delete the duplicate** automatically.
3.  **Fan-out:** You still get the benefit of sending one message to multiple independent services (Fraud, Shipping), but now they all get the messages in the **exact same order**.

---

### **Exam "Cheat Sheet" for your notes:**

| Feature | Standard SNS/SQS | FIFO SNS/SQS |
| :--- | :--- | :--- |
| **Ordering** | Best-effort (might be out of order). | **Guaranteed strict order.** |
| **Delivery** | At-least-once (might get duplicates). | **Exactly-once** (deduplication). |
| **Throughput** | Nearly unlimited. | Limited (but high enough for most apps). |
| **Suffix** | No special name. | **Must end in `.fifo`** (e.g., `orders.fifo`). |

---

### **SAA-C03 Exam "Triggers":**
*   If the question mentions **"ordering is critical"** or **"no duplicates allowed"** $\rightarrow$ **Pick FIFO.**
*   If the question asks to fan-out to multiple queues **while maintaining order** $\rightarrow$ **SNS FIFO + SQS FIFO.**

---


### SNS - Message Filtering 


### **SNS Message Filtering (The "Selective Listener")**

*   **The Concept:** A subscriber (like an SQS Queue) can set a **JSON Filter Policy**. SNS will then check the **Attributes** (metadata) of a message and only "push" it to that subscriber if it matches the criteria.
*   **The Mechanism:**
    1.  **Publisher (Buying Service):** Sends a message AND attaches **Message Attributes** (e.g., `State: Placed` or `State: Cancelled`).
    2.  **SNS Topic:** Receives the message and looks at the attributes.
    3.  **The Filter:** SNS compares the attributes against the Filter Policy on each subscription.
    4.  **Delivery:**
        *   If it matches $\rightarrow$ Message is delivered.
        *   If it doesn't match $\rightarrow$ Message is dropped for that specific subscriber.
        *   **No Policy?** $\rightarrow$ If a subscription has no filter, it receives **every** message by default (like the "SQS Queue (All)" at the bottom of the image).

---

### **Exam Summary for your notes:**

| Feature | SNS Message Filtering |
| :--- | :--- |
| **Logic Location** | Defined on the **Subscription**, not the Topic. |
| **Format** | **JSON Policy**. |
| **Benefit** | **Efficiency.** The Consumer (SQS/Lambda) doesn't waste CPU/money processing or deleting messages it doesn't need. |
| **Trigger Words** | "Filter messages based on attributes," "Subscriber only needs a subset of data." |

---

Think of this like **`grep`** for your messages.
*   **SNS Topic:** A stream of logs.
*   **Filter Policy:** `grep "ERROR"` or `grep "CANCELLED"`. 
*   Instead of your application reading the whole log file and searching for the word, SNS only hands you the lines you actually asked for.

