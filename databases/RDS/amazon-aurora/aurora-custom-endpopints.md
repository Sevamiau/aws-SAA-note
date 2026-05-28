# Aurora Custom Endpoints

----------

**Aurora Custom Endpoints** allow you to group specific database instances together under a unique DNS name. 

While the standard "Reader Endpoint" sends traffic to **all** replicas, a **Custom Endpoint** only sends traffic to a **subset** of instances that you choose.

### Why use them? (The "Short" Reason)
It allows you to **isolate workloads** so they don't interfere with each other.

### The 3 Main Use Cases:
1.  **Reporting vs. Web Traffic:** You can point your heavy, slow "Monthly Reports" to one high-memory instance, while your fast "Web App" traffic goes to three smaller instances.
2.  **Instance Sizing:** If you have a mix of large and small replicas in the same cluster, you can create a Custom Endpoint that only points to the **Large** instances for performance-heavy tasks.
3.  **Global Database:** In a Global Database setup, you can use Custom Endpoints to route traffic to specific regions.

### How it works:
*   You choose which instances belong to the "Custom" group.
*   AWS provides a unique URL (e.g., `my-custom-endpoint.cluster-xyz.aws.com`).
*   The endpoint **load-balances** traffic across only the instances in that specific group.

**Think of it as:** A VIP lane for specific types of traffic so they don't get stuck behind "regular" traffic.

----------

