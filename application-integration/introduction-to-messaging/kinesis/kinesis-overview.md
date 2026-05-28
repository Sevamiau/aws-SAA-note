# **Amazon Kinesis Data Streams (KDS)**

- Retention between up to 364 days 
- Ability to reprocess (replay) data by consumers 
- Data cant be deleted from Kinesis (until expires)
- Data up to 10MiB (typical use case is lot of "small" real time data)
- Data ordering gauarantee for data with the same "Partition ID"
- At-rest KMS encryption, in-flight HTTPS encryption 
- Kinesis Producer Library (KPL) to write and optimized producer application 
- Kinesis Client Library (KLC) to write an optimized consumer application 

## Kinesis Data Streams - Capacity Modes 

- Provisioned Mode 
    * Choose number of shards 
    * Each shard gets 1MB/s in (or 1000 records pers second)
    * Each shard gets 2MB/s out 
    * Scale manually to increase or decrease the number of shards 
    * You pay per shard Provisioned per hour 

- On-demand Mode:
    * No need to provision or manage the Capacity
    * default capacity provisioned (4 MB/s in or 4000 records per second)
    * Scales automatically based on observed throughput peak during last 30 days 
    * Pay per stream per hour & data in/out per GB 

*   **Official Description:** A scalable and durable real-time data streaming service that can continuously capture gigabytes of data per second from hundreds of thousands of sources.
*   **The Core Concept: Shards.**
    *   A stream is made of "Shards." 
    *   **1 Shard** gives you: **1 MB/s** Inbound (Write) and **2 MB/s** Outbound (Read).
    *   To get more speed, you add more shards (**Resharding**).
*   **Capacity Modes:**
    *   **Provisioned:** You choose the number of shards (Cheaper if you know your traffic).
    *   **On-Demand:** AWS scales the shards for you (Better if traffic is unpredictable).
*   **Data Retention:** Data stays in the stream for **24 hours by default** (up to 365 days). You can **"Replay"** the data as many times as you want during that time.

---

### **SAA-003 "Cheat Sheet": SQS vs. Kinesis**
This is the most common "Trap" on the exam. Use this table to decide:

| Feature | SQS (Simple Queue) | Kinesis Data Streams |
| :--- | :--- | :--- |
| **Data Usage** | Once a message is read, it's **deleted**. | Multiple consumers can read the **same data**. |
| **Replay** | Cannot replay messages. | **Can replay data** (Retention). |
| **Ordering** | Only FIFO SQS has order. | **Ordering is guaranteed** at the shard level. |
| **Scale** | Infinite (No management). | Scaled by **Shards** (Manual or On-demand). |
| **Use Case** | Decoupling apps / Workers. | **Real-time Analytics**, IoT, Clickstreams. |

---

### **Exam "Trigger Words" for Kinesis Data Streams:**
*   **"Real-time analytics"** (under 200ms latency).
*   **"Replay data"** or "Reprocess old data."
*   **"Multiple applications reading the same stream."**
*   **"Log aggregation from thousands of sources."**

---


