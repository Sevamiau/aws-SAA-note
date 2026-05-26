### **AWS FSx: The Four Flavors**

| FSx Type | Protocol | **The "Magic" Key Phrase** | **Use Case** |
| :--- | :--- | :--- | :--- |
| **Windows** | **SMB** | "Microsoft Active Directory" | Native Windows apps, shared `Z:` drives. |
| **Lustre** | **POSIX** | "HPC" or "Machine Learning" | Super-fast processing; reads/writes to **S3**. |
| **NetApp ONTAP** | **NFS, SMB, iSCSI** | "SnapMirror" or "Multi-protocol" | Hybrid Cloud; migrating existing NetApp arrays. |
| **OpenZFS** | **NFS** | "Sub-millisecond latency" | Specialized Linux apps needing extreme speed. |

---

### **1. FSx for Windows File Server**
*   **Protocol:** SMB only.
*   **Key Feature:** Fully managed Windows server. Supports Windows-specific features like **Shadow Copies** (recovery) and **ACLs**.
*   **The Exam Scenario:** "You need to migrate a Windows-based file share that requires **Active Directory** integration."

### **2. FSx for Lustre (The "Speed Demon")**
*   **Protocol:** POSIX (Linux-native).
*   **The "Scratch" Mode:** Can be used as a temporary high-speed buffer.
*   **The S3 Link:** It can "mount" an S3 bucket, turn the files into a fast file system, process them, and then save the results back to S3.
*   **The Exam Scenario:** "A video editing or **Machine Learning** team needs to process massive datasets from S3 at millions of IOPS."

### **3. FSx for NetApp ONTAP (The "Hybrid Bridge")**
*   **Protocols:** NFS, SMB, and iSCSI (the only one that does all three).
*   **Magic Features:** **Deduplication** (saves space/money) and **SnapMirror** (easy replication from on-prem to AWS).
*   **The Exam Scenario:** "A company uses NetApp on-premise and wants a **Hybrid** solution that works exactly the same in the cloud."

### **4. FSx for OpenZFS**
*   **Protocol:** NFS.
*   **The Vibe:** It's the "middle ground" between EFS and Lustre. It's built on ZFS (highly reliable Linux file system).
*   **The Exam Scenario:** "You need to migrate a Linux workload that requires **extremely low latency (sub-millisecond)** but doesn't need the massive scale of Lustre."

---

### **How to Choose**
If you see **FSx** in the answers, look for these **Triggers**:
1.  Is there a **Windows** requirement? $\rightarrow$ **FSx for Windows**.
2.  Is there a **NetApp** or **iSCSI** requirement? $\rightarrow$ **FSx for NetApp ONTAP**.
3.  Is it for **Machine Learning/HPC** or mentions **S3 integration**? $\rightarrow$ **FSx for Lustre**.
4.  Does it mention **sub-millisecond latency** for **Linux**? $\rightarrow$ **FSx for OpenZFS**.

**Important Comparison Note:**
*   **EFS:** General-purpose, simple Linux share (NFS).
*   **FSx:** Specialized, high-performance, or Windows/NetApp specific.

