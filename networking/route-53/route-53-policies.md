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

----------

## Routing Policies - IP based routing 

If Geolocation is **"Where are you on the map?"** and Latency is **"How fast are you?"**, then **IP-Based Routing** is **"What is your exact ID?"**

This is the newest routing policy (added in 2022). It allows you to take total control and tell AWS: *"If a user comes from exactly these IP addresses, send them here."*

### 1. How it works (The Manual Map)
In Geolocation, AWS "guesses" where a user is based on their IP. In **IP-Based Routing**, YOU provide the map.
1.  You create a **CIDR Collection** (a list of IP ranges like `181.16.0.0/16` for an Argentine ISP).
2.  You tell Route 53: *"Anyone in this collection goes to Server A."*
3.  Anyone else (not in your list) goes to the **Default** record.

### 2. Why use it? (The "Special Knowledge" Case)
The SAA-C03 exam loves to ask why you'd pick this over the "automatic" options:
*   **ISP Optimization:** You know that a specific internet provider in Argentina has a very expensive connection to your USA server. You use IP-based routing to force all users from that ISP to your local server in Brazil to save money.
*   **Custom Overrides:** Sometimes AWS's Geolocation map is wrong (it thinks a user is in Chile but they are in Argentina). You can use IP-based routing to manually "fix" it for those specific users.
*   **Internal Tools:** Routing your own office's IP range to a "Beta" version of your app while the rest of the world sees the "Production" version.

---

### 3. Geolocation vs. Latency vs. IP-Based
Think of it like choosing a restaurant:
*   **Geolocation:** "Show me restaurants in Buenos Aires." (Based on **Location**).
*   **Latency:** "Show me the restaurant that can deliver my food the fastest." (Based on **Speed**).
*   **IP-Based:** "If my friend 'Juan' calls, send him to my favorite grill. Everyone else goes to the pizza place." (Based on **Identity/Recognition**).

---

### 4. The "C" / Linux Logic: The `switch` Statement
Think of it like a `switch` statement in C or a manually edited **Static Route** in your **MikroTik**:

```c
switch(client_ip_range) {
    case ISP_TELECOM_AR:
        return BRAZIL_SERVER;
    case OFFICE_WIFI:
        return BETA_SERVER;
    default:
        return USA_SERVER; // The "Default" location
}
```

### SAA-C03 "Exam Trap":
*   **IP-Based** is **NOT** for Private Hosted Zones (only Public).
*   **EDNS Client Subnet (ECS):** This is a technical term you might see. It's a feature that allows Route 53 to "see" the actual user's IP even if they are using a middleman (resolver). IP-based routing uses this to be extra accurate.

### Summary:
*   **Latency:** Automatic speed (Use for general performance).
*   **Geolocation:** Automatic location (Use for language/laws).
*   **IP-Based:** **Manual CIDR control** (Use for ISP-specific rules or when you know your network better than AWS does).

Does that clarify why we have a 3rd option? It's the "Manual Mode" for people who want to override the "Automatic" logic of AWS!

- Routing is based on client's IP addresses 
- You provied a list of CIDR's for your clients and the corresponding endpoints/locations (user-IP-to-endpoint mappings)
- Use cases: Optimize performance, reduce network costs.

- Example: Route end users form a particular ISP to a specific endpoint 

----------

## Routing policies - Multi-value


### 1. The "Simple" Way (The Problem)
Is a **Simple Routing** record, you can put multiple IP addresses in one list (e.g., `1.1.1.1`, `2.2.2.2`).
*   **The Problem:** DNS just gives the user the whole list. DNS **does not know** if `2.2.2.2` is dead. 
*   **The Result:** If Server B crashes, the user's browser might still try to connect to it and fail.

### 2. The "Multi-Value" Way (The Solution)
**Multi-Value Answer Routing** is like Simple Routing, but it adds **Health Checks** to every single IP.

*   **The Scenario:** You have 8 web servers. You create a Multi-Value record for each one.
*   **The Action:** Route 53 is constantly "pinging" all 8 servers.
*   **The Result:** When a user asks for `api.example.com`, Route 53 looks at its list and says: *"Servers 1, 3, and 5 are healthy. Servers 2, 4, 6, 7, and 8 are dead. I will give the user up to 8 healthy IPs."*

---

### 3. How is it different from a Load Balancer?
This is exactly what Stephane Maarek might skip:
*   **Load Balancer:** One single IP address that manages the traffic.
*   **Multi-Value DNS:** Returns a **list of up to 8 healthy IP addresses** directly to the user's browser. The browser then picks one to connect to.

It is **Client-Side Load Balancing**. Instead of AWS doing the balancing, AWS gives the "client" (the browser) a list of healthy options and says: *"Pick one of these; they are all alive."*

---

### 5. Why use it? (The SAA-C03 Use Case)
*   **Availability:** It’s a very cheap way to get basic high availability without paying for an expensive Application Load Balancer (ALB).
*   **Low Latency:** Since there is no "middleman" (Load Balancer), the user connects directly to the server's IP.

---

### Comparison Summary:
*   **Simple:** Just a list. No health checks. (If a server dies, the user gets an error).
*   **Weighted:** You control the percentages (70/30).
*   **Multi-Value:** Up to 8 **Healthy** IPs. Randomly selected from the pool of survivors.
----------

