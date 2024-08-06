# PostgreSQL isolation level

PostgreSQL's default transaction isolation level is **Read Committed**.

This isolation level allows a transaction to read only data that has been committed before the transaction started.

- prevents ***dirty reads***
- allows for ***non-repeatable reads*** and ***phantom reads***.

[Isolation: Transactional isolation levels](Isolation%20Transactional%20isolation%20levels%20e0ccdbbcf6f3446a97b12cb1621f54ea.md)

> In Read Committed isolation level, each query within a transaction sees a snapshot of the database as of the time the query begins.
> 
> 
> This means that if a transaction reads the same data multiple times within the same transaction, it may see different values if another committed transaction has modified the data in between the reads.
> 

---

You can change the isolation level for a specific transaction in PostgreSQL using the `SET TRANSACTION` command followed by the desired isolation level:

```sql
BEGIN;
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
-- Perform your transaction operations
COMMIT;
```

PostgreSQL supports the following transaction isolation levels:

1. Read Uncommitted: This is the lowest isolation level, allowing transactions to read data modified by other transactions even if they are not committed yet. However, PostgreSQL treats Read Uncommitted the same as Read Committed, effectively preventing dirty reads.
2. Read Committed (default): Transactions can only read data that has been committed prior to the transaction's start time, preventing dirty reads but still allowing non-repeatable reads and phantom reads.
3. Repeatable Read: Transactions see a consistent snapshot of the database as of the time the transaction began, preventing dirty reads and non-repeatable reads. However, phantom reads are still possible.
4. Serializable: This is the highest isolation level, ensuring full transaction isolation by preventing dirty reads, non-repeatable reads, and phantom reads. Serializable transactions in PostgreSQL are implemented using Serializable Snapshot Isolation (SSI), which detects and rolls back transactions that would cause serialization anomalies.

Remember that while higher isolation levels provide better consistency, they may also negatively impact concurrency and performance due to increased locking or conflict detection. It's essential to choose the appropriate isolation level based on your application's requirements for consistency, concurrency, and performance.