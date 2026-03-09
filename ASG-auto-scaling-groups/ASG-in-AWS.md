# Auto Scaling Groups in AWS

In AWS Auto Scaling Groups (ASG), these three settings define the **boundaries** and the **target** for your fleet of servers (EC2 instances).


### 1. Minimum Capacity (The Floor)
*   **What it is:** The absolute smallest number of instances that must be running at all times.
*   **Why it exists:** To ensure your application can always handle at least some basic level of traffic, even when things are quiet.

### 2. Desired Capacity (The Target)
*   **What it is:** The specific number of instances you want running **right now**. AWS will constantly work to maintain this exact number.
*   **Why it exists:** This is the number that **scaling policies** actually change. If your CPU usage goes up, the scaling policy increases the "Desired Capacity" by 1, and AWS immediately launches a new instance to match it.

### 3. Maximum Capacity (The Ceiling)
*   **What it is:** The absolute most instances the group is allowed to launch, no matter how high the demand gets.
*   **Why it exists:** Primarily for **cost control**. It prevents your AWS bill from exploding if there is a sudden traffic spike or a "runaway" scaling event.


Minimum and Maximum are REQUIRED: You must define the floor and the ceiling so AWS knows the absolute boundaries of your scaling.[1]

Desired is OPTIONAL: If you don't specify a "Desired" number, AWS will simply default it to your Minimum.[2]

    Example: If you set Min: 2 and Max: 10, but leave Desired blank, AWS sets Desired to 2 and launches 2 instances immediately.
---

### Summary Table

| Setting | Purpose | Rule |
| :--- | :--- | :--- |
| **Minimum** | Availability | ASG will never go *below* this. |
| **Desired** | Operational Target | ASG will always try to *match* this. |
| **Maximum** | Cost Control | ASG will never go *above* this. |

**Pro Tip:** Your **Desired Capacity** must always be between your Minimum and Maximum values (e.g., Min: 2, Desired: 4, Max: 10).
