# SNS to Amazon S3 trough Kinesis Data Firehose 



### **SNS → Kinesis Data Firehose → S3**

*   **The Concept:** SNS is great for sending "live" notifications, but it doesn't store them. If you want to **keep a record** of every notification that passes through your SNS Topic, you "subscribe" Kinesis Data Firehose to that topic.
*   **The Workflow:**
    1.  **SNS Topic:** Receives the "Purchase" or "Event" message.
    2.  **Kinesis Data Firehose (KDF):** Grabs the message. It can **batch** many messages together (e.g., wait until it has 1MB of data or 60 seconds have passed).
    3.  **Amazon S3:** KDF dumps the batch of messages into an S3 bucket for long-term storage or analysis.

---

### **Why use this? (The SAA-C03 Logic)**

1.  **Archiving:** You need a permanent record of all notifications for legal or audit reasons.
2.  **Analytics:** You want to run a report later on all the "Buying Service" events using a tool like **Amazon Athena** (which reads data directly from S3).
3.  **No Code Required:** This is a "Managed" integration. You don't need to write a Lambda function to move the data; AWS handles the "pipe" between SNS and S3 for you.

---

### **Exam Summary for your notes:**

| Feature | SNS to Kinesis Firehose |
| :--- | :--- |
| **Main Goal** | **Store** or **Analyze** SNS messages long-term. |
| **Trigger Word** | "Capture/Archive SNS messages to S3." |
| **Kinesis Firehose Role** | Acts as a "delivery stream" that batches and moves data to a destination (S3, Redshift, etc.). |

---

