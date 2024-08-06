# Consistency

Consistency can mean different things in cloud/software engineering, depending on the context.

In the case of ACID, the “C” was most likely added to make the acronym work 🙂.

Consistency in the context of ACID means *consistency in data*, which is defined by the creator of the database.

<aside>
<img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" /> Consistency in database systems refers to the requirement that any given database transaction must change affected data only in allowed ways.

⇒ *The technical term for consistency in data is called **Referential Integrity**.*

</aside>

Referential integrity is a method of ensuring that relationships between tables  remain consistent. It's usually enforced through the use of foreign keys.

![Untitled](Fullstack/Relational/Consistency%20a53755ad08664f14b87cdb8b798877eb/Untitled.png)

<aside>
<img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" /> For a database to be consistent, data written to the database must be valid according to all defined rules, including constraints, cascades, triggers, or any combination.

</aside>

Consistency does not guarantee correctness of the transaction in all ways an application programmer might expect (that is the responsibility of application-level code).

Instead, consistency merely guarantees that programming errors cannot result in the violation of any defined database constraints.