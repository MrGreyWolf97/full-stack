# Isolation: Transactional isolation levels

Transactional levels, also known as **Isolation levels**, are a concept in database management systems that determine the degree of isolation between multiple transactions executing concurrently.

They control the visibility of changes made by one transaction to other concurrently running transactions.

Isolation levels help balance the need for concurrent access to data while preventing issues like dirty reads, non-repeatable reads, and phantom reads.

---

## Read Uncommitted

[SET TRANSACTION ISOLATION LEVEL (Transact-SQL) - SQL Server](https://learn.microsoft.com/en-us/sql/t-sql/statements/set-transaction-isolation-level-transact-sql?view=sql-server-ver16)

This is the lowest isolation level, where statements can read rows that have been modified by other transactions but not yet committed..

Transactions running at the **Read Uncommitted** level:

- do not issue shared locks to prevent other transactions from modifying data read by the current transaction
- are not blocked by exclusive locks that would prevent the current transaction from reading rows that have been modified but not committed by other transactions

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Pros

High concurrency as transactions can access modified data without waiting for other transactions to complete.

</aside>

<aside>
<img src="https://www.notion.so/icons/snippet_red.svg" alt="https://www.notion.so/icons/snippet_red.svg" width="40px" /> Cons

Susceptible to:

- **dirty reads**
- **non-repeatable reads**
- **phantom reads**
</aside>

---

## Read Committed

[Read Committed Isolation Level](https://www.postgresql.org/docs/7.2/xact-read-committed.html)

> When a transaction runs on this isolation level, a **SELECT** query sees only data committed before the query began and never sees either uncommitted data or changes committed during query execution by concurrent transactions.
> 

> Notice that **two successive SELECTs can see different data**, even though they are within a single transaction, when other transactions commit changes during execution of the first **SELECT**.
> 

> Each query does see the effects of previous updates executed within this same transaction, even though they are not yet committed.
> 

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Pros

Provides a reasonable level of consistency while maintaining good concurrency.

---

Prevents:

- **dirty reads**
</aside>

<aside>
<img src="https://www.notion.so/icons/snippet_red.svg" alt="https://www.notion.so/icons/snippet_red.svg" width="40px" /> Cons

Susceptible to:

- **non-repeatable reads**
- **phantom reads**
</aside>

---

## Repeatable Read

[13.2. Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html#XACT-REPEATABLE-READ)

> The *Repeatable Read* isolation level only sees data committed before the transaction began; it never sees either uncommitted data or changes committed by concurrent transactions during the transaction's execution.
> 

> This level is different from Read Committed in that a query in a repeatable read transaction sees a snapshot as of the start of the first non-transaction-control statement in the *transaction*, ***not as of the start of the current statement*** within the transaction.
> 

> Each query does see the effects of previous updates executed within its own transaction, even though they are not yet committed.
> 

This isolation level ensures that once a transaction reads data, it sees the same data if it reads it again, preventing non-repeatable reads.

It does so by placing locks on the data being read, preventing other transactions from modifying it until the current transaction is complete.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Pros

Provides a high level of consistency.

---

Prevents:

- **dirty reads**
- **non-repeatable reads**
</aside>

<aside>
<img src="https://www.notion.so/icons/snippet_red.svg" alt="https://www.notion.so/icons/snippet_red.svg" width="40px" /> Cons

May suffer of **reduced concurrency** due to ***locking***.

---

Susceptible:

- **phantom reads**
</aside>

---

## Serializable

[13.2. Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html#XACT-SERIALIZABLE)

This level emulates serial transaction execution for all committed transactions; as if transactions had been executed one after another, serially, rather than concurrently.

Like the Repeatable Read level, applications using this level must be prepared to retry transactions due to serialization failures. In fact, this isolation level works exactly the same as Repeatable Read except that it also monitors for conditions which could make execution of a concurrent set of serializable transactions behave in a manner inconsistent with all possible serial (one at a time) executions of those transactions.

This monitoring does not introduce any blocking beyond that present in repeatable read, but there is some overhead to the monitoring, and detection of the conditions which could cause a *serialization anomaly* will trigger a *serialization failure*.

This is the highest isolation level, where transactions are fully isolated from one another. It prevents dirty reads, non-repeatable reads, and phantom reads by requiring transactions to execute in a strictly serial order or by using strict locking mechanisms. Serializable ensures the highest level of consistency but can have a significant impact on concurrency and performance.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Pros

Ensures full transaction isolation and provides the highest level of consistency.

Prevents:

- **dirty reads**
- **non-repeatable reads**
- **phantom reads**
</aside>

<aside>
<img src="https://www.notion.so/icons/snippet_red.svg" alt="https://www.notion.so/icons/snippet_red.svg" width="40px" /> Cons

Can lead to **reduced concurrency and performance** due to ***strict locking*** or ***serial execution***.

</aside>

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Choosing the appropriate transaction isolation level depends on the specific requirements of the application in terms of consistency, concurrency, and performance.

***Lower isolation levels offer higher concurrency at the expense of consistency, while higher levels provide better consistency but may negatively impact concurrency and performance.***

</aside>