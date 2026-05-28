# Auto Scaling Group in AWS with Load Balancers


### 1. Automatic Registration (The New Arrival)
When the ASG decides to launch a new instance (because your traffic went up), it doesn't just leave it sitting there. It automatically "registers" that new instance with the Load Balancer's **Target Group**.

### 2. Health Checks (The Quality Control)
By default, an ASG only checks if the server is "powered on" (EC2 Health Check). But if you connect it to a Load Balancer, you can turn on **ELB Health Checks**. 
*   The Load Balancer sends a "ping" to the instance (e.g., "Are you still alive?") every few seconds.
*   If the instance stops responding (maybe the app crashed even though the server is "on"), the Load Balancer tells the ASG: "This instance is broken."
*   The ASG then **terminates** the broken instance and **launches** a fresh one.

### 3. Connection Draining (The Graceful Exit)
When the ASG needs to scale down (remove an instance), it doesn't just pull the plug instantly. It uses **Deregistration Delay** (also called Connection Draining).
*   The Load Balancer stops sending *new* requests to that instance.
*   It gives the instance a few minutes to finish the requests it is currently processing.
*   Once it's "drained" of all active users, the ASG safely shuts it down.

---

### In Summary:
*   **ASG's Job:** Make sure the right number of instances exist (The Management).
*   **Load Balancer's Job:** Distribute traffic only to the healthy ones (The Traffic Cop).
*   **The Connection:** The **Target Group** is the "list" that links them together.

**Why use them together?** Without the Load Balancer, your users wouldn't know which of your 10 instances to connect to. Without the ASG, your Load Balancer would eventually be sending traffic to "ghost" servers that have crashed. Together, they make your app **Self-Healing** and **Scalable**.
