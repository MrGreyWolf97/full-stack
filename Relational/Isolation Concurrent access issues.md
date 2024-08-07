# Isolation: Concurrent access issues

Concurrent access in a database system can lead to several issues when multiple transactions are executing simultaneously.

These issues can affect the data's consistency and correctness.

The main issues related to concurrent access are:

1. ***Dirty Read***
A dirty read occurs when a transaction reads data that has been modified by another transaction but has not yet been committed. This can lead to inconsistencies, as the reading transaction may see an intermediate state of the data, which could be rolled back later.
2. ***Non-repeatable Read***
A non-repeatable read occurs when a transaction reads the same data more than once within the same transaction, and the data has been modified by another committed transaction in between the reads.
This can lead to inconsistencies, as the reading transaction may see different values for the same data at different points in time.
3. ***Phantom Read***
A phantom read occurs when a transaction reads a set of data (e.g., a range of rows) more than once within the same transaction, and *new data has been added* or *existing data has been deleted* by another committed transaction in between the reads.
This can lead to inconsistencies, as the reading transaction may see new records (phantom records) or miss existing records that were present during the first read but not in the subsequent reads.
4. ***Lost Update***
A lost update occurs when two transactions read and modify the same data concurrently, and **one of the transactions' updates is lost** because the other transaction overwrites it.
This can lead to inconsistencies, as the final state of the data may not accurately reflect the intended updates from both transactions.
5. ***Write Skew***
Write skew occurs when two transactions read the same data and make different decisions based on that data, but each transaction updates a different part of the data.
As a result, both updates are committed, leading to an inconsistent state that would not have occurred if the transactions were executed serially.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> To mitigate these concurrent access issues, database systems use various techniques:

[Isolation: Transactional isolation levels](Isolation%20Transactional%20isolation%20levels.md)

- locking
- versioning
</aside>