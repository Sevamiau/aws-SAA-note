# Aurora Replicas - Auto Scaling

----------

**Aurora Replica Auto Scaling** automatically adjusts the number of read-only nodes in your cluster based on actual traffic.


*   **What it does:** It adds more Replicas when traffic is high and removes them when traffic drops (to save money).
*   **How it works:** You set a "Target Tracking" policy. For example: *"Keep my average CPU at 70%."*
*   **Metrics used:** Usually based on **Average CPU Utilization** or **Average Connections** across all readers.
*   **The Limit:** It can scale up to a maximum of **15 replicas**.
*   **The Best Part:** When a new replica is added, the **Reader Endpoint** automatically starts sending traffic to it—you don’t have to change any code.

**Crucial Note:** It only scales **Readers**. It does **not** scale the Master/Writer node. To scale the Writer, you would typically use *Aurora Serverless v2*.

----------

