
# **DSSE-KMS (Dual-Layer Server-Side Encryption)**

*   **The Concept:** It applies **two independent layers** of server-side encryption to objects at the same time.
*   **The "Why":** It is designed to meet **CNSA 2.0** (Commercial National Security Algorithm) standards. It protects against the "what if one encryption algorithm is cracked?" scenario.
*   **Who uses it?** Primarily government, defense, or highly regulated industries that require the absolute highest level of data protection.
*   **Key Requirement:** It uses **AWS KMS** (specifically Customer Managed Keys) to manage the keys for both layers.

---

### **Exam "Cheat Sheet" for DSSE-KMS:**

| Keyword in Question | Correct Answer |
| :--- | :--- |
| **"CNSA 2.0 Compliance"** | **DSSE-KMS** |
| **"Double encryption" at the object level** | **DSSE-KMS** |
| **"Two independent layers of encryption"** | **DSSE-KMS** |

**How it differs from SSE-KMS:**
*   **SSE-KMS:** 1 layer of encryption.
*   **DSSE-KMS:** 2 layers of encryption. (Higher cost due to more KMS API calls, but higher security).

**Note:** You enable this in the S3 Bucket settings or via a `PUT` request header. Like other KMS-based encryption, it also provides an audit trail in **CloudTrail**.
