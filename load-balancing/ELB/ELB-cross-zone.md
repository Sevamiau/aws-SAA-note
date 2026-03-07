# Cross-Zone Load Balancing

-Cross-zone load balancing allows a load balancer to distribute traffic evenly across all registered instances in all enabled Availability Zones, rather than just the instances in its own local zone.

-Application Load Balancer
    * Enabled by default (can be disable at the target group level)
    *No charges for inter AZ data. Usually AWS if data goes across AZ's you have to pay

-Network and Gateway Load Balancers
    *Disabled by default
    *You pay charges for inter AZ data if enabled

-Classic Load Balancer
    *Disabled by default
    *No charges for inter AZ data if enabled

-When **Cross-Zone Load Balancing** is enabled, the Load Balancer ignores the AZ boundaries and treats all instances as one big pool.

### The Math (Example)
Imagine you have **10 instances** total: 2 in AZ-A and 8 in AZ-B.

*   **With Cross-Zone ON (Distributes by Instance):**
    Each of the 10 instances gets **10%** of the traffic. It is perfectly balanced across your servers.

*   **With Cross-Zone OFF (Distributes by AZ):**
    The traffic is split 50/50 between the two AZs first. 
    *   The 2 instances in AZ-A share 50% of the traffic (**25% each**).
    *   The 8 instances in AZ-B share 50% of the traffic (**6.25% each**).
    *   *Result:* The servers in AZ-A are working 4x harder than the servers in AZ-B!

### Summary:
*   **ON:** Focuses on the **Instance** (Even wear and tear on all servers).
*   **OFF:** Focuses on the **AZ** (Even split between data centers, but can cause "hot" servers).

**Pro Tip:** This is why it is **always ON by default** for the Application Load Balancer (ALB)—it’s almost always what you want for web traffic.
