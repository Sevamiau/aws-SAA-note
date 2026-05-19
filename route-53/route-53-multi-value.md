# Multi value


### 1. The "Simple" Way (The Problem)
In a **Simple Routing** record, you can put multiple IP addresses in one list (e.g., `1.1.1.1`, `2.2.2.2`).
*   **The Problem:** DNS just gives the user the whole list. DNS **does not know** if `2.2.2.2` is dead. 
*   **The Result:** If Server B crashes, the user's browser might still try to connect to it and fail.

### 2. The "Multi-Value" Way (The Solution)
**Multi-Value Answer Routing** is like Simple Routing, but it adds **Health Checks** to every single IP.

*   **The Scenario:** You have 8 web servers. You create a Multi-Value record for each one.
*   **The Action:** Route 53 is constantly "pinging" all 8 servers.
*   **The Result:** When a user asks for `api.example.com`, Route 53 looks at its list and says: *"Servers 1, 3, and 5 are healthy. Servers 2, 4, 6, 7, and 8 are dead. I will give the user up to 8 healthy IPs."*

---

### 3. How is it different from a Load Balancer?
*   **Load Balancer:** One single IP address that manages the traffic.
*   **Multi-Value DNS:** Returns a **list of up to 8 healthy IP addresses** directly to the user's browser. The browser then picks one to connect to.

It is **Client-Side Load Balancing**. Instead of AWS doing the balancing, AWS gives the "client" (the browser) a list of healthy options and says: *"Pick one of these; they are all alive."*

---

