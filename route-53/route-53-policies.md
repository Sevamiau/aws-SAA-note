# Route 53 - Routing policies

----------

- Define how Route 53 responds to DNS queries 
- Dont get confused by the word "Routing"
  * Its not the same as load balances routing which routes the traffic
  * DNS ***DO NOT***  route any traffic, it only responds to the DNS queries 

- Route 53 Supports the following Routing policies:
  * Simple
  * Weighted
  * Failover
  * Latency based
  * Geolocation
  * Multi-value Answer
  * Geoproximity (using route 53 traffic flow feature)

----------
  
## Routing policies - **Simple**

- Typically, route, traffic, to a single resource
- Can specify multiple values in the same record
- If multiple values are returned, a random one is chosen by the client
- When Alias enabled, specify only one AWS resource
- Cant be associated with Health Checks

----------

## Routing policies - Weighted 

- Control the % of the requests that go to each specific source 
- Assign each record a relative weight 
  * Weights dont need to sum up 100
- DNS records must have the same name and type
- Can be associated with Health Checks 
- Use Cases: Load balancing between regions, testing, new apps versions.
- Assign a weight of 0 to a record to spot sending traffic to a resource 
- If all records have weight of 0, then all records will be returned equally


Why use it? (The "Canary" Test)

This is the main reason for the SAA-C03 exam:

    Canary Deployment: You have a new version of your app (Version 2). You don't want to send everyone there yet because it might have a bug.

    The Strategy: You set Version 1 to Weight 95 and Version 2 to Weight 5.

    If your logs look good and Version 2 doesn't crash, you slowly change the weights to 50/50, and eventually 0/100.

----------

## Routing policies - Latency-based 

- Redirect to the resource that has the least latency close to us 
- Super helpful when latency for users is a priority 
- Latency is based on traffic between users and AWS Regions 
- Germany users may be directed to US (if thats the lowest latency)
- Can be associated with Health Checks (has a failover capability) 


----------


## Routing policies - Failover


The **Failover Routing Policy** in Route 53 is used to create an **Active-Passive** setup. It is your "Plan B" strategy for disaster recovery.

### 1. What it does
It ensures that if your main website or application goes down, your users are automatically redirected to a backup version (like a standby server in another region or a static "Under Maintenance" page in S3).

### 2. How it works
You create two records with the same name (e.g., `app.example.com`):

1.  **Primary Record:** This is your "Active" resource. All traffic goes here by default.
2.  **Secondary Record:** This is your "Passive" (backup) resource. It sits idle and receives no traffic unless the Primary fails.
3.  **The Health Check:** You must associate a **Health Check** with the Primary record. Route 53 constantly pings your primary resource to see if it’s alive.

**The Logic:**
*   **If Primary is Healthy:** Route 53 sends 100% of traffic to the **Primary**.
*   **If Primary is Unhealthy:** Route 53 automatically switches and sends 100% of traffic to the **Secondary**.
*   **When Primary Recovers:** Route 53 detects it is healthy again and automatically shifts traffic back to the **Primary**.

### 3. Key Difference from other policies
Unlike **Weighted Routing** (which splits traffic by percentage) or **Multivalue Answer** (which acts like a mini-load balancer), Failover is **all-or-nothing**. It is designed purely for reliability, not for spreading load.

### Simple Rule of Thumb:
Use **Failover Routing** for **Disaster Recovery**. It is the "Panic Button" that automatically flips the switch to your backup site if your main site crashes.


----------

## Routing Policies - Geolocation

- Different from Latency-based
- This routing is based on user location 
- Specify location by continent, country, or bu US state (if theres overlapping most precise location selected)
- Should create a "default" record (in case thres no match on location)
- Use cases: Website localization, restrict content distribution, load balancing.
- Can be associated with Health Checks 


if the question mentions "Compliance," "Legal restrictions," or "Localized content," choose Geolocation.

If the question mentions "Global user base," "Minimize delay," or "Improve performance," choose Latency.

----------


## Routing Policies - Geoproximity

- Route traffic to your resources based o the geographic location of users and resources 
- Ability **to shift more traffic to resources based** in the define bias.
- To change the size of the geographic region specify bias values:
  * To expand (1-99) - More traffic to the resource 
  * To shrink (-1-99) - Less traffic to the resource 

- Resources can be:
  * AWS resources (specify AWS region)
  * Non-AWS resources (specify latitude and longitude)

- You must used Route 53 advance option Traffic Flow to use this feature.  
