
### **AWS Messaging Services: SQS vs. SNS vs. Kinesis**

| Feature | **Amazon SQS** | **Amazon SNS** | **Amazon Kinesis** |
| :--- | :--- | :--- | :--- |
| **Delivery Model** | **PULL** (Consumers pull data). | **PUSH** (SNS pushes to many subs). | **PULL** (Standard) or **PUSH** (Enhanced). |
| **Persistence** | Data is **deleted** after consumption. | **None.** Data is lost if not delivered. | **Yes (Replay).** Data expires after X days. |
| **Consumers** | Multiple workers for one queue. | Up to 12.5 million subscribers (Pub/Sub). | Multiple consumers read the same stream. |
| **Throughput** | No need to provision (Auto-scales). | No need to provision (Auto-scales). | **Provisioned** (Shards) or **On-demand**. |
| **Ordering** | Only on **FIFO** queues. | SQS FIFO integration for ordering. | Guaranteed at the **Shard level**. |
| **Main Use Case** | **Decoupling** and work buffers. | **Fan-out**, alerts, and notifications. | **Real-time Big Data**, analytics, and ETL. |
| **Special Feature** | Individual message delay capability. | Up to 100,000 topics. | Can **replay/reprocess** old data. |

---

### **One last note on Amazon MQ (The final topic):**
Since you are about to hit the quiz, just remember this one thing about **Amazon MQ**:
*   **The "Legacy" Service:** Use this only when a company wants to migrate to AWS but **cannot change their code** to use SQS/SNS. 
*   **Protocols:** It supports industry-standard protocols like **MQTT, AMQP, and STOMP** (which SQS/SNS do not). 
*   **The Answer:** If the exam mentions "Migrating a RabbitMQ or ActiveMQ cluster with minimal code changes," the answer is **Amazon MQ**.

Good luck with the quiz! You're almost at the finish line for today. Get some sleep—your brain will process all this "messaging" logic while you rest. **See you Tuesday!**
