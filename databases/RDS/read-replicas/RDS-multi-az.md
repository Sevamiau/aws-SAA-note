# RDS Multi AZ (Disaster Recovery)

----------

While a **Read Replica** is for **Performance**, **Multi-AZ** is for **Survival**.

If Read Replicas are like "printing extra copies of a newspaper" (so more people can read), Multi-AZ is like a **Spare Tire** in your car.

### 1. The Goal: High Availability (HA)
The primary purpose of Multi-AZ (Multiple Availability Zones) is to ensure your database stays online even if a data center explodes or a server fails. It is **not** for scaling; it is for **reliability**.

### 2. How it Works: Synchronous Replication
*   AWS creates a "Standby" database in a different Availability Zone (a separate data center).
*   **Synchronous:** Every time you write data to your Main DB, AWS waits for the Standby DB to confirm it has the data too. They are **exact twins** at all times.
*   **Invisible:** You cannot connect to the Standby DB. It is just sitting there "in the dark," waiting for an emergency.

### 3. Automatic Failover (The Magic Part)
If your Main DB crashes or the data center loses power:
1.  AWS detects the failure immediately.
2.  AWS automatically points your database URL (endpoint) to the Standby DB.
3.  The Standby becomes the new Primary.
4.  **No work for you:** Your application doesn't need a code change; it just keeps working after a short 60–120 second pause.

---

**Simple Rule of Thumb:** 
*   Use **Read Replicas** when your DB is **too slow**. 
*   Use **Multi-AZ** when your DB **must never go down**. 

*(Note: In production, it is very common to use **both** at the same time!)*
