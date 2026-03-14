# Global Aurora

----------

- Aurora Cross Region Read Replicas:
    * Useful for disaster recovery
    * Simple to put in place 

- Aurora Global Database ( recommended )
  * 1 primary region (read/write)
  * Up to 10 secondary (read-only) regions, replication lag is less than 1 second
  * Up to 16 Read Replicas per secondary region
  * Helps for decreasing latency 
  * Promoting another region (for disaster recovery) has an RTO (recovery time Objective) of < 1 minute
  * Typical cross-region replication takes less than 1 second
----------


-**Amazon Aurora Global Database** is a feature that allows a single Aurora database to span multiple AWS Regions. It is designed for globally distributed applications with high availability and fast disaster recovery requirements.

Here is the "really short" breakdown:

### 1. How it’s Structured
*   **Primary Region:** One region acts as the "Home" where your application performs all **Writes**.
*   **Secondary Regions:** You can have up to **5 secondary regions**. Each secondary region contains its own Aurora cluster that stays in sync with the primary.

### 2. Sub-Second Replication
*   **Storage-Based:** Unlike traditional databases that use the "compute" (CPU) to replicate data, Global Aurora uses the **storage layer**. 
*   **Speed:** It replicates data across the world with a typical latency of **less than 1 second**. Because it happens at the storage level, it doesn't slow down your primary database performance.

### 3. Key Benefits
*   **Low-Latency Reads:** Users in Europe can read from a local European replica instead of waiting for data to travel from a US-based master.
*   **Disaster Recovery (DR):** If an entire AWS Region goes offline (e.g., US-East-1), you can promote a secondary region (e.g., EU-West-1) to be the new "Master" in **less than 1 minute**.
*   **RPO/RTO:** It provides a Recovery Point Objective (RPO) of about 1 second and a Recovery Time Objective (RTO) of under a minute.

### 4. Write Forwarding
If an application in a secondary region accidentally tries to "Write" to its local (read-only) replica, Aurora can automatically **forward** that write back to the Primary Region for you. This makes coding global apps much simpler.

**Summary:** Think of it as **"The World-Wide Database."** It keeps your data synchronized globally so that if one part of the world goes dark, your app stays online using another region.
