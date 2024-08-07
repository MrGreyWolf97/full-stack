# JPA pessimistic locking
## [Overview](https://www.baeldung.com/jpa-pessimistic-locking#overview)

There are plenty of situations when we want to retrieve data from a database.
==Sometimes we want to lock it for ourselves for further processing so no one else can interrupt our actions.==

**We can think of two concurrency control mechanisms that allow us to do that:**
1. setting the proper *Transaction Isolation Level*
2. setting a *Lock* on data that we need at the moment.

The transaction isolation is defined for database connections.
We can configure it to retain the different degree of locking data.

However, **the isolation level is set once the connection is created**, and it affects every statement within that connection. Luckily, we can use pessimistic locking, which uses database mechanisms for reserving more granular exclusive access to the data.

We can use a pessimistic lock to ensure that no other transactions can modify or delete reserved data.

There are two types of locks we can retain: an exclusive lock and a shared lock. We could read but not write in data when someone else holds a shared lock. In order to modify or delete the reserved data, we need to have an exclusive lock.

We can acquire exclusive locks using _‘SELECT … FOR UPDATE’_ statements.

## 2. Lock Modes[](https://www.baeldung.com/jpa-pessimistic-locking#lock-modes)

JPA specification defines three pessimistic lock modes that we’re going to discuss:

- _PESSIMISTIC_READ_ allows us to obtain a shared lock and prevent the data from being updated or deleted.
- _PESSIMISTIC_WRITE_ allows us to obtain an exclusive lock and prevent the data from being read, updated or deleted.
- _PESSIMISTIC_FORCE_INCREMENT_ works like _PESSIMISTIC_WRITE_, and it additionally increments a version attribute of a versioned entity.

All of them are static members of the _LockModeType_ class and allow transactions to obtain a database lock. They all are retained until the transaction commits or rolls back.

**It’s worth noting that we can obtain only one lock at a time. If it’s impossible, a _PersistenceException_ is thrown.**

### 2.1. _PESSIMISTIC_READ_[](https://www.baeldung.com/jpa-pessimistic-locking#1-pessimisticread)

Whenever we want to just read data and don’t encounter dirty reads, we could use _PESSIMISTIC_READ_ (shared lock). **We won’t be able to make any updates or deletes, though.**

It sometimes happens that the database we use doesn’t support the _PESSIMISTIC_READ_ lock, so we could obtain the _PESSIMISTIC_WRITE_ lock instead.

### 2.2. _PESSIMISTIC_WRITE_[](https://www.baeldung.com/jpa-pessimistic-locking#2-pessimisticwrite)

Any transaction that needs to acquire a lock on data and make changes to it should obtain the _PESSIMISTIC_WRITE_ lock. According to the _JPA_ specification, holding _PESSIMISTIC_WRITE_ lock will prevent other transactions from reading, updating or deleting the data.

**Please note that some database systems implement [multi-version concurrency control](https://en.wikipedia.org/wiki/Multiversion_concurrency_control) that allows readers to fetch data that has been already blocked.**

### 2.3. _PESSIMISTIC_FORCE_INCREMENT_[](https://www.baeldung.com/jpa-pessimistic-locking#3-pessimisticforceincrement)

This lock works similarly to _PESSIMISTIC_WRITE_, but it was introduced to cooperate with versioned entities — entities that have an attribute annotated with _@Version_.

Any updates of versioned entities could be preceded with obtaining the _PESSIMISTIC_FORCE_INCREMENT_ lock. **Acquiring that lock results in updating the version column.**

It’s up to a persistence provider to determine whether it supports _PESSIMISTIC_FORCE_INCREMENT_ for unversioned entities or not. If it doesn’t, it throws the _PersistenceException_.

### 2.4. Exceptions[](https://www.baeldung.com/jpa-pessimistic-locking#4-exceptions)

It’s good to know which exception may occur while working with pessimistic locking. _JPA_ specification provides different types of exceptions:

- _PessimisticLockException_ indicates that obtaining a lock or converting a shared to exclusive lock fails and results in a transaction-level rollback.
- _LockTimeoutException_ indicates that obtaining a lock or converting a shared lock to exclusive times out and results in a statement-level rollback.
- _PersistenceException_ indicates that a persistence problem occurred. _PersistenceException_ and its subtypes, except _NoResultException_, _NonUniqueResultException_, _LockTimeoutException_ and _QueryTimeoutException_, **mark the active transaction to be rolled back.**

## 3. Using Pessimistic Locks[](https://www.baeldung.com/jpa-pessimistic-locking#using-pessimistic-locks)

**There are a few possible ways to configure a pessimistic lock on a single record or group of records.** Let’s see how to do it in JPA.

### 3.1. Find[](https://www.baeldung.com/jpa-pessimistic-locking#1-find)

Find is probably the most straightforward way.

It’s enough to pass a _LockModeType_ object as a parameter to the _find_ method:

```java
entityManager.find(Student.class, studentId, LockModeType.PESSIMISTIC_READ);
```

### 3.2. Query[](https://www.baeldung.com/jpa-pessimistic-locking#2-query)

Additionally, we can use a _Query_ object as well and call the _setLockMode_ setter with a lock mode as a parameter:

```java
Query query = entityManager.createQuery("from Student where studentId = :studentId");
query.setParameter("studentId", studentId);
query.setLockMode(LockModeType.PESSIMISTIC_WRITE);
query.getResultList()
```

### 3.3. Explicit Locking[](https://www.baeldung.com/jpa-pessimistic-locking#3-explicit-locking)

It’s also possible to manually lock the results retrieved by the find method:

```java
Student resultStudent = entityManager.find(Student.class, studentId);
entityManager.lock(resultStudent, LockModeType.PESSIMISTIC_WRITE);
```

### 3.4. Refresh[](https://www.baeldung.com/jpa-pessimistic-locking#4-refresh)

If we want to overwrite the state of the entity by the _refresh_ method, we can also set a lock:

```java
Student resultStudent = entityManager.find(Student.class, studentId);
entityManager.refresh(resultStudent, LockModeType.PESSIMISTIC_FORCE_INCREMENT);
```

### 3.5. NamedQuery[](https://www.baeldung.com/jpa-pessimistic-locking#5-namedquery)

_@NamedQuery_ annotation allows us to set a lock mode as well:

```java
@NamedQuery(name="lockStudent",
  query="SELECT s FROM Student s WHERE s.id LIKE :studentId",
  lockMode = PESSIMISTIC_READ)
```

## 4. Lock Scope[](https://www.baeldung.com/jpa-pessimistic-locking#lock-scopes)

**Lock scope parameter defines how to deal with locking relationships of the locked entity.** It’s possible to obtain a lock just on a single entity defined in a query or additionally block its relationships.

To configure the scope, we can use _PessimisticLockScope_ enum. It contains two values: _NORMAL_ and _EXTENDED_.

We can set the scope by passing a parameter _‘jakarta.persistence’_ with _PessimisticLockScope_ value as an argument to the proper method of _EntityManager_, _Query_, _TypedQuery_ or _NamedQuery_:

```java
Map<String, Object> properties = new HashMap<>();
map.put("jakarta.persistence", PessimisticLockScope.EXTENDED);
    
entityManager.find(
  Student.class, 1L, LockModeType.PESSIMISTIC_WRITE, properties);
```

### 4.1. _PessimisticLockScope.NORMAL_[](https://www.baeldung.com/jpa-pessimistic-locking#1-pessimisticlockscopenormal)

**The _PessimisticLockScope.NORMAL_ is the default scope.** With this locking scope, we lock the entity itself. When used with joined inheritance, it also locks the ancestors.

Let’s look at the sample code with two entities:

```java
@Entity
@Inheritance(strategy = InheritanceType.JOINED)
public class Person {

    @Id
    private Long id;
    private String name;
    private String lastName;

    // getters and setters
}

@Entity
public class Employee extends Person {

    private BigDecimal salary;

    // getters and setters
}
```

When we want to obtain a lock on the _Employee_, we can observe the _SQL_ query that spans over those two entities:

```sql
SELECT t0.ID, t0.DTYPE, t0.LASTNAME, t0.NAME, t1.ID, t1.SALARY 
FROM PERSON t0, EMPLOYEE t1 
WHERE ((t0.ID = ?) AND ((t1.ID = t0.ID) AND (t0.DTYPE = ?))) FOR UPDATE
```

### 4.2. _PessimisticLockScope.EXTENDED_[](https://www.baeldung.com/jpa-pessimistic-locking#2-pessimisticlockscopeextended)

The _EXTENDED_ scope covers the same functionality as _NORMAL_. In addition, **it’s able to block related entities in a join table.**

Simply put, it works with entities annotated with _@ElementCollection_ or _@OneToOne_, _@OneToMany_, etc. with _@JoinTable_.

Let’s look at the sample code with the _@ElementCollection_ annotation:

```java
@Entity
public class Customer {

    @Id
    private Long customerId;
    private String name;
    private String lastName;
    @ElementCollection
    @CollectionTable(name = "customer_address")
    private List<Address> addressList;

    // getters and setters
}

@Embeddable
public class Address {

    private String country;
    private String city;

    // getters and setters
}
```

Let’s analyze some queries when searching for the _Customer_ entity:

```sql
SELECT CUSTOMERID, LASTNAME, NAME 
FROM CUSTOMER WHERE (CUSTOMERID = ?) FOR UPDATE

SELECT CITY, COUNTRY, Customer_CUSTOMERID 
FROM customer_address 
WHERE (Customer_CUSTOMERID = ?) FOR UPDATE
```

We can see that there are two _FOR UPDATE_ queries that lock a row in the customer table as well as a row in the join table.

**Another interesting fact to note is that not all persistence providers support lock scopes.**

## 5. Setting Lock Timeout[](https://www.baeldung.com/jpa-pessimistic-locking#setting-timeout)

Besides setting lock scopes, we can adjust another lock parameter — timeout. **The timeout value is the number of milliseconds that we want to wait for obtaining a lock until the _LockTimeoutException_ occurs.**

We can change the value of timeout similarly to lock scopes, by using property _‘jakarta.persistence.lock.timeout’_ with the proper number of milliseconds.

It’s also possible to specify “no wait” locking by changing timeout value to zero.

However, we should keep in mind that there are database drivers that **don’t support setting a timeout value this way**:

```java
Map<String, Object> properties = new HashMap<>(); 
map.put("jakarta.persistence.lock.timeout", 1000L); 

entityManager.find(
  Student.class, 1L, LockModeType.PESSIMISTIC_READ, properties);
```


---

***References***
- [Baeldung article](https://www.baeldung.com/jpa-pessimistic-locking)