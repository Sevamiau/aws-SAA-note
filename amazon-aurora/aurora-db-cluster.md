# Aurora DB cluster

----------

### 1. The Endpoints (The Entry Points)
At the top, you see the **Client** (your application) connecting to two different boxes. This is how you manage traffic:
*   **Writer Endpoint (Green):** Your application uses this DNS address for all **Write** operations (INSERT, UPDATE, DELETE). It always points specifically to the Master (M) node.
*   **Reader Endpoint (Orange):** Your application uses this for **Read** operations (SELECT). It acts as a **Load Balancer**, automatically spreading your read requests across all the available Replicas (R) so one single instance doesn't get overwhelmed.

### 2. The Master Node (M)
*   The node labeled **"M"** is the **Primary/Writer instance**.
*   There is only **one** master per cluster. 
*   Notice the **"W"** arrow pointing down: It is the only instance allowed to change or add data to the shared storage volume.

### 3. The Aurora Replicas (R)
*   The nodes labeled **"R"** are **Read Replicas**.
*   They are read-only. You can have up to 15 of them.
*   **Auto Scaling (The Blue Arrow):** This indicates that Aurora can automatically add more "R" nodes if your traffic spikes, or remove them if traffic drops, to save you money.

### 4. Shared Storage Volume (The Black Arrow)
This is the most important part of the Aurora design:
*   **Decoupled Storage:** Unlike traditional databases where every instance has its own disk, here **all nodes share the same storage**.
*   **Auto Expanding:** You don't have to worry about running out of space. As you add data, the volume grows automatically in small increments. (The diagram says up to **256 TB**; note that in some regions/versions, this limit is currently 128 TB).
*   **High Availability:** While not pictured, this shared volume is actually replicated 6 times across 3 different Data Centers (Availability Zones).

### Why this architecture is "Better":
1.  **Fast Failover:** If the Master (**M**) dies, Aurora simply points the **Writer Endpoint** to one of the Replicas (**R**). Since they all share the same storage, there is no need to "sync" data, and the failover happens in seconds.
2.  **Performance:** Because the Replicas aren't busy doing their own "writes" to their own disks, they are much faster at serving read requests.
3.  **Simplicity:** Your application only needs two URLs (the Endpoints). You don't need to track the IP addresses of the individual database servers.


----------

