# ACID

ACID is an acronym that stands for Atomicity, Consistency, Isolation, and Durability.

These principles are essential in guaranteeing the reliability of database transactions, particularly in the context of distributed systems.

---

### Atomicity

This principle ensures that a transaction is either fully completed or not executed at all.

In other words, ***if any part of the transaction fails, the entire transaction is rolled back*** to its initial state, as if it never happened.

This guarantees that the database remains in a consistent state even after encountering errors or failures.

### Consistency

Consistency requires that a database must always transition from one consistent state to another.

> A ***Consistent state*** is when all the:
> 
> - data integrity constraints
> - business rules
> - other validation checks
> 
> are satisfied
> 

If a transaction violates these rules, it must be aborted to maintain consistency.

### Isolation

This principle ensures that the transactions are isolated from one another, meaning that **the concurrent execution of multiple transactions does not affect each other's outcome**.

Each transaction should be executed as if it is the only transaction running in the system.

> This is achieved through various concurrency control mechanisms, which prevent data conflicts and maintain data integrity, such as:
> 
> - locking
> - versioning

### Durability

Durability guarantees that **once a transaction is committed, the changes it made to the database are permanent**, even in the case of system failures or crashes.

This is typically achieved by storing ***transaction logs***, which can be used to recover and reconstruct the committed state of the database after a failure.