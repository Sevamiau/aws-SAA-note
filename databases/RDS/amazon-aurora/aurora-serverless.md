# Aurora Serverless

----------

- Automated database instatiation and auto scaling based on actual usage

**Aurora Serverless** is an on-demand, auto-scaling configuration where the database automatically adjusts its capacity (CPU and RAM) based on your application's actual needs.

### 1. How it Scales (The "Magic")
*   **ACUs (Aurora Capacity Units):** Instead of picking a server size (like `db.r5.large`), you set a **range** (e.g., Min: 0.5 ACU – Max: 16 ACU). Each ACU is roughly 2GB of RAM.
*   **Instant & Granular:** Unlike traditional scaling that requires a reboot, Aurora Serverless v2 scales in **milliseconds**. It increases or decreases in tiny increments (0.5 ACU) without dropping connections.

### 2. Cost Efficiency
*   **Pay-per-second:** You only pay for the capacity the database is *actually* using at that moment.
*   **Scaling to Zero:** As of late 2024, Serverless v2 can **pause completely** (0 ACUs) when there are no connections, meaning you pay $0 for compute while it's idle. It "wakes up" in about 15 seconds when a new request comes in.

### 3. When to use it
*   **Unpredictable Workloads:** Great for apps where you don't know when traffic will spike.
*   **Development/Test:** Perfect for environments that aren't used 24/7.
*   **Low-Traffic Apps:** Cheaper than keeping a provisioned "Always On" server for an app that only gets a few hits an hour.

### 4. Provisioned vs. Serverless (Quick Mix)
You can actually **mix them** in the same cluster. You can have a "Provisioned" Master for steady traffic and "Serverless" Replicas that only scale up to help during heavy bursts.

**Summary:** Think of it like a **utility bill**. You don't pay for a giant water tank; you just pay for the water that actually comes out of the faucet.
----------

