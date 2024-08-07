# Atomicity

Atomicity is a property of database transactions that ensures that a set of database operations either all occur, or none occur.

This is important because it allows database transactions to be isolated from one another, ensuring that they are atomic, or indivisible.

<aside>
<img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" /> In other words, if one part of a database transaction fails, the entire transaction will be rolled back, or undone, to its original state.

</aside>

![Untitled](Relational/Atomicity/Untitled.png)

There are several benefits to this type of database behaviour.

- It ensures the consistency of the database.
If a database transaction is not atomic, it is possible for the data in the database to become corrupted, as some operations may be completed while others are not.
This can lead to inconsistencies in the data and can make it difficult or impossible to accurately retrieve and manipulate the data.
- It helps to protect the integrity of the database.
If a database transaction is not atomic, it is possible for a database to become corrupt if one part of the transaction succeeds while another part fails.
This can lead to data loss or other problems that can be difficult or impossible to recover from.
- It helps to ensure that database transactions are performed in a timely and efficient manner.
If a database transaction is not atomic, it may take longer to complete, as the database may have to roll back the transaction and start over if one part of the transaction fails.
This can lead to slower performance and decreased efficiency.

In order to ensure atomicity in databases, transactions must be carefully designed and implemented.
This typically involves using a combination of database locks, commit and rollback statements, and other techniques to ensure that all parts of a database transaction are completed successfully.

It is important to note that atomicity is just one of several important properties of database transactions, along with ***consistency, isolation, durability***.

Together, these properties form the foundation of database transaction management and help to ensure the reliability and integrity of database systems.

---

***References***

- https://www.beekeeperstudio.io/blog/what-is-atomicity-in-databases