## [Transaction Isolation](https://www.baeldung.com/spring-transactional-propagation-isolation#transactional-isolations)

Isolation is one of the common ACID properties: Atomicity, Consistency, Isolation, and Durability. Isolation describes how changes applied by concurrent transactions are visible to each other.

Each isolation level prevents zero or more concurrency side effects on a transaction:

- **Dirty read:** read the uncommitted change of a concurrent transaction
- **Non-repeatable read**: get different value on re-read of a row if a concurrent transaction updates the same row and commits
- **Phantom read:** get different rows after re-execution of a range query if another transaction adds or removes some rows in the range and commits

We can set the isolation level of a transaction by _@Transactional::isolation._ It has these five enumerations in Spring: _DEFAULT_, _READ_UNCOMMITTED_, _READ_COMMITTED_, _REPEATABLE_READ_, _SERIALIZABLE._

### [Isolation Management in Spring](https://www.baeldung.com/spring-transactional-propagation-isolation#1-isolation-management-in-spring)

The default isolation level is _DEFAULT_. As a result, when Spring creates a new transaction, the isolation level will be the default isolation of our RDBMS. Therefore, we should be careful if we change the database.

We should also consider cases when we call a chain of methods with different isolation_._ In the normal flow, the isolation only applies when a new transaction is created. Thus, if for any reason we don’t want to allow a method to execute in different isolation, we have to set _TransactionManager::setValidateExistingTransaction_ to true.

Then the pseudo-code of transaction validation will be:

```java
if (isolationLevel != ISOLATION_DEFAULT) {
    if (currentTransactionIsolationLevel() != isolationLevel) {
        throw IllegalTransactionStateException
    }
}
```


---

#### [1. _READ_UNCOMMITTED_ Isolation](https://www.baeldung.com/spring-transactional-propagation-isolation#2-readuncommitted-isolation)

_READ_UNCOMMITTED_ is the lowest isolation level and allows for the most concurrent access.

As a result, it suffers from all three mentioned concurrency side effects. A transaction with this isolation reads uncommitted data of other concurrent transactions. Also, both non-repeatable and phantom reads can happen. Thus we can get a different result on re-read of a row or re-execution of a range query.

We can set the _isolation_ level for a method or class:

```java
@Transactional(isolation = Isolation.READ_UNCOMMITTED)
public void log(String message) {
    // ...
}
```

**Postgres does not support _READ_UNCOMMITTED_ isolation and falls back to _READ_COMMITED_ instead.** **Also, Oracle does not support or allow _READ_UNCOMMITTED_.  
**

---
#### [2. _READ_COMMITTED_ Isolation](https://www.baeldung.com/spring-transactional-propagation-isolation#3-readcommitted-isolation)

The second level of isolation, _READ_COMMITTED,_ prevents dirty reads.

The rest of the concurrency side effects could still happen. So uncommitted changes in concurrent transactions have no impact on us, but if a transaction commits its changes, our result could change by re-querying.

Here we set the _isolation_ level:

```java
@Transactional(isolation = Isolation.READ_COMMITTED)
public void log(String message){
    // ...
}
```

**_READ_COMMITTED_ is the default level with Postgres, SQL Server, and Oracle.**

---
#### [3. _REPEATABLE_READ_ Isolation](https://www.baeldung.com/spring-transactional-propagation-isolation#4-repeatableread-isolation)

The third level of isolation, _REPEATABLE_READ,_ prevents dirty, and non-repeatable reads. So we are not affected by uncommitted changes in concurrent transactions.

Also, when we re-query for a row, we don’t get a different result. However, in the re-execution of range-queries, we may get newly added or removed rows.

Moreover, it is the lowest required level to prevent the lost update. The lost update occurs when two or more concurrent transactions read and update the same row. _REPEATABLE_READ_ does not allow simultaneous access to a row at all. Hence the lost update can’t happen.  

Here is how to set the _isolation_ level for a method:

```java
@Transactional(isolation = Isolation.REPEATABLE_READ) 
public void log(String message){
    // ...
}
```

**_REPEATABLE_READ_ is the default level in Mysql.** **Oracle does not support _REPEATABLE_READ_.**

---
#### [4. _SERIALIZABLE_ Isolation](https://www.baeldung.com/spring-transactional-propagation-isolation#5-serializable-isolation)

_SERIALIZABLE_ is the highest level of isolation. It prevents all mentioned concurrency side effects, but can lead to the lowest concurrent access rate because it executes concurrent calls sequentially.

In other words, concurrent execution of a group of serializable transactions has the same result as executing them in serial.

Now let’s see how to set _SERIALIZABLE_ as the _isolation_ level:

```java
@Transactional(isolation = Isolation.SERIALIZABLE)
public void log(String message){
    // ...
}
```

---
***References***
- [Baeldung article](https://www.baeldung.com/spring-transactional-propagation-isolation)