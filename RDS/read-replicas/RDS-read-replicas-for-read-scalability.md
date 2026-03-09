# RDS Read Replicas for read Scalability


An **RDS Read Replica** is a "read-only" copy of your primary database. Its main job is to take the "viewing" load off your main database so it doesn't get overwhelmed.

---

- How it Works
 * **Asynchronous Replication:** When you write data to your Primary DB, AWS automatically copies that data to the Read Replica. (There is usually a tiny delay of a few seconds).
 * **Offloading Traffic:** You point your application's "SELECT" (read) queries to the Replica's endpoint and keep "INSERT/UPDATE" (write) queries on the Primary.
 * **Scaling:** You can create up to **15 replicas** for a single database to handle massive amounts of read traffic.

---

- Why use it? (Benefits)
*   **Read Scalability:** If your app has millions of users looking at data (like a social media feed), replicas stop the main DB from crashing.
*   **Performance:** Heavily complex "read" reports won't slow down the "write" operations for your customers.
*   **Global Reach:** You can put a replica in a different country (Cross-Region) so local users can read data faster.

**Concise Summary:** Use Read Replicas when your database is slow because too many users are **looking** at data at the same time.
