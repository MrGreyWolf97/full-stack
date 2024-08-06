# Isolation: Locking

Database locking is a mechanism used in Relational Database Management Systems (RDBMS) to ensure data consistency and protect the integrity of data during concurrent access by multiple users.

It helps to prevent data conflicts, data loss, and other issues that could arise when multiple transactions are trying to read, update, or delete data simultaneously.

Locks work by letting only one transaction modify or access a certain database object.

This makes it look like the transactions are executed one after the other and hence maintaining data integrity.

<aside>
<img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" /> In a relational database, locks can be applied at different levels depending on the RDBMS and the configuration settings.

- row-level
- page-level
- table-level
</aside>

---

### Lock Types

1. **Shared Lock** (Read Lock)
This lock is applied when a transaction wants to read data from a database object (e.g., row, page, or table).
Multiple transactions can acquire shared locks on the same resource simultaneously, allowing *concurrent reads* but preventing other transactions from *modifying the data*.
⇒ *No transaction is allowed to update the resource while it has a shared lock*
2. **Exclusive Lock** (Write Lock)
This lock is applied when a transaction wants to modify data (e.g., insert, update, or delete) in a database object.
Exclusive locks are not compatible with other exclusive locks or shared locks on the same resource.
⇒ *Only one transaction can acquire an exclusive lock on a certain resource at one point in time*

Summary:

- Multiple shared locks can be acquired on a resource at one time.
But if the resource already has a shared lock then another process cannot acquire an exclusive lock on it.
- A process cannot acquire a shared lock on a resource that is locked by an exclusive lock.

---

### Locking Process

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> When a transaction wants to access a database object, it requests the appropriate lock type (shared or exclusive) from the database management system.

</aside>

The RDBMS evaluates the request based on the **current locks** held by other transactions and the **isolation level** defined for the transaction.

If the requested lock:

1. is compatible (with the existing locks): the RDBMS grants the lock, and the transaction proceeds to access the data.
2. is not compatible (with the existing locks): the requesting transaction is blocked and put into a waiting state until the conflicting lock is released.

---

### Optimistic vs Pessimistic Locking

**Optimistic locking**

It assumes that resource conflicts are rare and allows transactions to proceed without acquiring locks initially.
⇒ *It checks for conflicts only at the commit time and **rolls back** the transaction if a conflict is detected*.

**Pessimistic locking**

It assumes that conflicts are likely and acquires locks upfront.

⇒ *A transaction has exclusive access to the resource during its execution*.

<aside>
<img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" /> ***Example***

In a transaction with multiple steps, having a pessimistic lock may not be a good idea since if the transaction locking the rows fails in between, the time that it spent has gone to waste. 

While in such scenarios if you have optimistic locking, other processes might be able to complete their transactions.

</aside>

Different relational databases may implement locking mechanisms differently, and understanding the locking behaviour of your specific RDBMS is crucial for optimizing performance and maintaining data integrity.

It is also essential to choose the appropriate transaction isolation level and locking strategy based on the specific requirements of your application.

---

### Problems associated with locks

1. ***Deadlocks***

Deadlocks can occur when two or more transactions are waiting for each other to release a lock.
To resolve deadlocks, RDBMS typically uses a combination of techniques such as timeouts, deadlock detection algorithms, and transaction rollbacks.

1. ***Lock Escalation***

Lock escalation is a technique used by some RDBMS to improve performance by converting many fine-grained locks (e.g., row-level locks) into a coarser lock (e.g., table-level lock) when the number of locks acquired by a transaction exceeds a certain threshold.

However, this can increase the chances of contention and reduce concurrency.

1. ***Lock contention***

There might be resources in a database that are accessed a lot.

A number of transactions might try to acquire locks on these resources.

As subsequent transactions have to wait for others to finish, there might be a delay in executing these transactions. This leads to the contention of these resources or locks — imagine single checkout counters in stores where everyone has to wait for their turn!

---

***References***

- https://medium.com/inspiredbrilliance/what-are-database-locks-1aff9117c290