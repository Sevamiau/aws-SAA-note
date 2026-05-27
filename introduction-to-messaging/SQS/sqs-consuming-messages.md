# SQS - Consuming Messages 

- Consumers (running on EC2 instances, servers, or AWS Lambda)
- Poll SQS for messages (receive up to 10 messages at a time)
- Process the messages (example: Insert the message into an RDS database)
- Delete the messages using the DeleteMessageAPI 

# SQS - Multiple EC2 Instances Consumers

- Consumers receive and process messages in parallel 
- At least once delivery
- Best-effort message ordering
- Consumers delete messages after processing them
- We can scale consumers horizontally to improve throughput of processing 


### **SQS: Decoupling Application Tiers**

*   **The Problem (Tight Coupling):** If your Front-end talks directly to your Back-end, and the Back-end crashes or gets overwhelmed, the whole website breaks.
*   **The Solution (Loose Coupling):** You place an **SQS Queue** as a buffer between the tiers.

---

### **The Architecture Flow (For your notes):**

1.  **Front-end Web App:** Receives user requests (e.g., "Upload this video") and immediately sends a message to **SQS**. It doesn't wait for the work to finish; it tells the user "Processing..." and moves to the next request.
2.  **SQS Queue:** Acts as a **durable buffer**. It holds the "work orders" safely. Even if the back-end is offline, the messages stay in the queue (up to 14 days).
3.  **Back-end Processing:** These instances "poll" SQS for work. They take one message at a time, process the video, and save the result to **S3**.
4.  **Independent Scaling:** 
    *   If many users arrive, the **Front-end ASG** scales up.
    *   If the **SQS Queue** gets too long, the **Back-end ASG** scales up to process the backlog faster.

---

### **Exam "Cheat Sheet" Benefits:**

| Feature | Why it matters |
| :--- | :--- |
| **Decoupling** | If the back-end fails, the front-end remains functional. |
| **Buffering** | Handles sudden spikes in traffic without crashing the servers. |
| **Independent Scaling** | You only pay for the "Compute" each tier actually needs. |
| **Data Integrity** | No requests are lost; they wait in the queue until processed. |

---


# SQS - Security 

- Encryption:
    * In-flight Encryption using HTTPS API 
    * At-rest Encryption using KMS keys 
    * Client-side Encryption if the client wants to perform Encryption/Decryption itself 

- Access Controls: IAM policies to regulate access to the SQS API 

- SQS Access policies (Similar to S3 bucket policies)
    * Useful for cross-account access to SQS queues
    * Useful for allowing other services (SNS,S3) to write to an SQS queue 
