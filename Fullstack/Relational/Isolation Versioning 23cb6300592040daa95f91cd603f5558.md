# Isolation: Versioning

Relational database versioning is a technique used to maintain a history of changes made to the data, allowing multiple users to access and modify the database concurrently without causing conflicts or consistency issues.

It is also known as Multi-Version Concurrency Control (MVCC) in some database management systems.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> MVCC works by creating s*eparate versions or snapshots of the data for each transaction*, instead of locking the data during the transaction execution.

When a transaction reads or modifies data, it operates on its snapshot, ensuring that other transactions can continue to work with their snapshots without being blocked or causing conflicts.

</aside>

---

Here's how MVCC can help prevent concurrent access issues and maintain data consistency:

### 1. Read Consistency

MVCC provides a consistent view of the data for each transaction by maintaining a snapshot of the data at the time the transaction started.

When a transaction reads data, it always retrieves the data from its snapshot, ensuring that it sees a consistent state of the data even if other transactions are modifying the data concurrently.

### 2. Write Consistency

When a transaction modifies data (e.g., insert, update, or delete), it creates a new version of the affected data in its snapshot.
This ensures that other transactions can continue to read the older version of the data without being affected by the changes made by the current transaction.

### 3. Isolation

MVCC provides isolation between transactions by ensuring that each transaction works with its snapshot, effectively separating the effects of one transaction from another.

This isolation helps prevent issues like dirty reads, non-repeatable reads, and phantom reads, which can occur when multiple transactions access and modify the same data concurrently.

### 4. Conflict Resolution

When multiple transactions try to modify the same data simultaneously, MVCC detects conflicts by comparing the version of the data being modified.

If two transactions attempt to modify the same data, the first transaction to commit its changes will succeed, while the second transaction will be required to resolve the conflict (e.g., by retrying the operation, merging changes, or aborting the transaction).

### 5. Reduced Locking

By maintaining separate snapshots for each transaction, MVCC allows multiple transactions to read and modify the data concurrently without the need for extensive locking.

This reduces lock contention and improves overall system performance and scalability.

It is important to note that the implementation of MVCC varies across different relational database management systems, and the specific details might differ depending on the system being used. Some popular databases that use MVCC include PostgreSQL, MySQL (with InnoDB storage engine), and Oracle.

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> **Summary**

Relational database versioning, or MVCC, helps prevent concurrent access issues and maintain data consistency by creating separate snapshots of the data for each transaction.

This allows multiple transactions to read and modify the data concurrently without causing conflicts or requiring extensive locking, improving overall system performance and scalability.

</aside>