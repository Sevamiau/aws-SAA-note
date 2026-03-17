# Elasticache User Session Store 


**It is a separate "Cluster" of Servers**

**ElastiCache is basically "Shared Memory" for the entire internet.** It allows thousands of separate servers to treat a single Redis/Memcached cluster as if it were one giant, shared global variable.
----------

In the world of Cloud Architecture, a **User Session Store** is a way to make your application **Stateless**.


### The Problem: The "Stateful" Mess
Imagine you have a website with a Load Balancer and 3 Web Servers.
1.  **User logs in:** The Load Balancer sends them to **Server A**.
2.  **Server A** creates a "Session" (a small piece of data saying "User 123 is logged in") and stores it in its **local RAM**.
3.  **The User clicks "View Profile":** The Load Balancer (doing its job) sends the request to **Server B**.
4.  **The Crash:** Server B looks at its own RAM, doesn't see a session, and says, *"I don't know who you are. Please log in again."*

**The "Old" Fix (Sticky Sessions):** You could force the Load Balancer to always send the same user to the same server. But if Server A crashes, the user is logged out anyway. This is not "High Availability."

---

### The Solution: ElastiCache Session Store
Instead of keeping the session inside the Web Server's local RAM, you move it to a **centralized ElastiCache cluster.**

1.  **User logs in:** The App writes the session data to **ElastiCache**.
2.  **User clicks "View Profile":** The Load Balancer sends them to **any** server (A, B, or C).
3.  **The Retrieval:** Whichever server receives the request simply asks ElastiCache: *"Hey, does User 123 have a session?"*
4.  **The Success:** ElastiCache says *"Yes,"* and the user stays logged in.

---

### Why ElastiCache is perfect for this:
*   **Speed:** Sessions need to be checked on every single click. Since ElastiCache is **RAM-based**, it can return that session data in under 1 millisecond.
*   **Expiration (TTL):** In C, you have to manually `free()` memory. In ElastiCache, you set a **Time To Live (TTL)**. If the user is inactive for 30 minutes, ElastiCache automatically deletes the session.
*   **Scalability:** You can scale your web servers from 3 to 3,000, and they can all share the same session store.

---



