# JPA query types

**There are three basic types of JPA Queries:**

- _Query_ => written in Java Persistence Query Language (JPQL) syntax
- _NativeQuery_ => written in plain SQL syntax
- _Criteria API Query_ => constructed programmatically via different methods

---

## [_Query_](https://www.baeldung.com/jpa-queries#query)

**A _Query_ is similar in syntax to SQL, and it’s generally used to perform CRUD operations:**

```java
public UserEntity getUserByIdWithPlainQuery(Long id) {
    Query jpqlQuery = getEntityManager().createQuery("SELECT u FROM UserEntity u WHERE u.id=:id");
    jpqlQuery.setParameter("id", id);
    return (UserEntity) jpqlQuery.getSingleResult();
}
```

This _Query_ retrieves the matching record from the _users_ table and also maps it to the _UserEntity_ object.

There are two additional _Query_ sub-types:
- _TypedQuery_
- _NamedQuery_


### [1. TypedQuery](https://www.baeldung.com/jpa-queries#1-typedquery)

We need to pay attention to the _return_ statement in our previous example.
JPA can’t deduce what the _Query_ result type will be, and, as a result, we have to cast.

But, **JPA provides a special _Query_ sub-type known as a _TypedQuery._**
This is always preferred if we know our _Query_ result type beforehand. Additionally, it makes our code much more reliable and easier to test.

Let’s see a _TypedQuery_ alternative, compared to our first example:

```java
public UserEntity getUserByIdWithTypedQuery(Long id) {
    TypedQuery<UserEntity> typedQuery
      = getEntityManager().createQuery("SELECT u FROM UserEntity u WHERE u.id=:id", UserEntity.class);
    typedQuery.setParameter("id", id);
    return typedQuery.getSingleResult();
}
```

This way, **we get stronger typing for free,** avoiding possible casting exceptions down the road.

### [2. NamedQuery](https://www.baeldung.com/jpa-queries#2namedquery)

While we can dynamically define a _Query_ on specific methods, they can eventually grow into a hard-to-maintain codebase.
What if we could keep general usage queries in one centralized, easy-to-read place?

JPA’s also got us covered on this with another _Query_ sub-type known as a _[NamedQuery](https://www.baeldung.com/hibernate-named-query)_.

We can define _NamedQueries_ in _orm.xml_ or a properties file.

**Also, we can define _NamedQuery_ on the _Entity_ class itself, providing a centralized, quick and easy way to read and find an _Entity_‘s related queries.**

All _NamedQueries_ must have a unique name.

Let’s see how we can add a _NamedQuery_ to our _UserEntity_ class:

```java
@Table(name = "users")
@Entity
@NamedQuery(name = "UserEntity.findByUserId", query = "SELECT u FROM UserEntity u WHERE u.id=:userId")
public class UserEntity {

    @Id
    private Long id;
    private String name;
    //Standard constructor, getters and setters.

}
```

**The _@NamedQuery_ annotation has to be grouped inside a _@NamedQueries_ annotation if we’re using Java before version 8.
From Java 8 forward, we can simply repeat the _@NamedQuery_ annotation at our _Entity_ class.**

Using a _NamedQuery_ is very simple:

```java
public UserEntity getUserByIdWithNamedQuery(Long id) {
    Query namedQuery = getEntityManager().createNamedQuery("UserEntity.findByUserId");
    namedQuery.setParameter("userId", id);
    return (UserEntity) namedQuery.getSingleResult();
}
```

---

## [NativeQuery](https://www.baeldung.com/jpa-queries#native-query)

**A _NativeQuery_ is simply an SQL query. These allow us to unleash the full power of our database, as we can use proprietary features not available in JPQL-restricted syntax.**

This comes at a cost. We lose the database portability of our application with _NativeQuery_ because our JPA provider can’t abstract specific details from the database implementation or vendor anymore.

Let’s see how to use a _NativeQuery_ that yields the same results as our previous examples:

```java
public UserEntity getUserByIdWithNativeQuery(Long id) {
    Query nativeQuery
      = getEntityManager().createNativeQuery("SELECT * FROM users WHERE id=:userId", UserEntity.class);
    nativeQuery.setParameter("userId", id);
    return (UserEntity) nativeQuery.getSingleResult();
}
```

We must always consider if a _NativeQuery_ is the only option. **Most of the time, a good JPQL _Query_ can fulfill our needs and most importantly, maintain a level of abstraction from the actual database implementation.**

Using _NativeQuery_ doesn’t necessarily mean locking ourselves to one specific database vendor. After all, if our queries don’t use proprietary SQL commands and are using only a standard SQL syntax, switching providers should not be an issue.

---

## [Query, NamedQuery, and NativeQuery](https://www.baeldung.com/jpa-queries#query-namedquery-and-nativequery)

So far, we’ve learned about _Query_, _NamedQuery_, and _NativeQuery_.

Now, let’s revisit them quickly and summarize their pros and cons.

### [1. Query](https://www.baeldung.com/jpa-queries#1-query)

We can create a query using _entityManager.createQuery(queryString)_.

Next, let’s explore the pros and cons of _Query_:

Pros:

- When we create a query using _EntityManager_, we can build dynamic query strings
- Queries are written in JPQL, so they’re portable

Cons:

- For a dynamic query, it may be compiled into a native SQL statement multiple times depending on the [query plan cache](https://www.baeldung.com/hibernate-query-plan-cache)
- The queries may scatter into various Java classes and they’re mixed in with Java code. Therefore, it could be difficult to maintain if a project contains many queries

### [2. NamedQuery](https://www.baeldung.com/jpa-queries#2-namedquery)

Once a _NamedQuery_ has been defined, we can reference it using the _EntityManager_:

```java
entityManager.createNamedQuery(queryName);
```

Now, let’s look at the advantages and disadvantages of _NamedQueries_:

Pros:

- _NamedQueries_ are compiled and validated when the persistence unit is loaded. That is to say, they’re compiled only once
- We can centralize _NamedQueries_ to make them easier to maintain – for example, in _orm.xml_, in properties files, or on _@Entity_ classes

Cons:

- _NamedQueries_ are always static
- _NamedQueries_ can be referenced in Spring Data JPA repositories. However, [dynamic sorting](https://www.baeldung.com/spring-data-sorting#sorting-with-spring-data) is not supported

### [3. NativeQuery](https://www.baeldung.com/jpa-queries#3-nativequery)

We can create a _NativeQuery_ using _EntityManager_:

```java
entityManager.createNativeQuery(sqlStmt);
```

Depending on the result mapping, we can also pass the second parameter to the method, such as an _Entity_ class, as we’ve seen in a previous example.

_NativeQueries_ have pros and cons, too. Let’s look at them quickly:

Pros:

- As our queries get complex, sometimes the JPA-generated SQL statements aren’t the most optimized. In this case, we can use _NativeQueries_ to make the queries more efficient
- _NativeQueries_ allow us to use database vendor-specific features. Sometimes, those features can give our queries better performance

Cons:

- Vendor-specific features can bring convenience and better performance, but we pay for that benefit by losing the portability from one database to another

---

## [Criteria API Query](https://www.baeldung.com/jpa-queries#criteria-api-query)

**[_Criteria_ API queries](https://www.baeldung.com/hibernate-criteria-queries) are programmatically-built, type-safe queries – somewhat similar to JPQL queries in syntax:**

```java
public UserEntity getUserByIdWithCriteriaQuery(Long id) {
    CriteriaBuilder criteriaBuilder = getEntityManager().getCriteriaBuilder();
    CriteriaQuery<UserEntity> criteriaQuery = criteriaBuilder.createQuery(UserEntity.class);
    Root<UserEntity> userRoot = criteriaQuery.from(UserEntity.class);
    UserEntity queryResult = getEntityManager().createQuery(criteriaQuery.select(userRoot)
      .where(criteriaBuilder.equal(userRoot.get("id"), id)))
      .getSingleResult();
    return queryResult;
}
```

It can be daunting to use _Criteria_ API queries first-hand, but they can be a great choice when we need to add dynamic query elements or when coupled with the [JPA _Metamodel_.](https://www.baeldung.com/hibernate-criteria-queries-metamodel)

---

## [Conclusion](https://www.baeldung.com/jpa-queries#conclusion)

In this quick article, we learned what JPA Queries are, along with their usage.

JPA Queries are a great way to abstract our business logic from our data access layer as we can rely on JPQL syntax and let our JPA provider of choice handle the _Query_ translation.

All code presented in this article is available [over on GitHub](https://github.com/eugenp/tutorials/tree/master/persistence-modules/java-jpa-2).
\

---

***References***
- [Baeldung article](https://www.baeldung.com/jpa-queries)