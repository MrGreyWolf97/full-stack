# Hibernate isolation

Hibernate is an Object-Relational Mapping (ORM) framework for Java applications that simplifies database access by mapping Java objects to database tables. It provides an abstraction over the underlying database system and offers various transaction isolation levels, depending on the database system being used.

By default, Hibernate does not enforce a specific isolation level. Instead, it relies on the default isolation level provided by the underlying database system (e.g., PostgreSQL, MySQL, Oracle). When a new connection is obtained from the connection pool, Hibernate uses the default isolation level set by the database system for that connection.

If you want to set a specific isolation level for Hibernate transactions, you can do so either at the application level or on a per-transaction basis:

1. Application level: You can configure the default isolation level for all Hibernate transactions by setting the `hibernate.connection.isolation` property in your Hibernate configuration (e.g., in the `hibernate.cfg.xml` file or `application.properties` file). The property value should be one of the standard JDBC `java.sql.Connection` constants, such as `TRANSACTION_READ_COMMITTED` or `TRANSACTION_SERIALIZABLE`.
    
    Example (in `application.properties`):
    
    ```xml
    spring.jpa.properties.hibernate.connection.isolation=2
    ```
    

2. Per-transaction basis: You can set the isolation level for a specific transaction using the `@Transactional` annotation (from the Spring Framework) on a method or class. The `isolation` attribute of the `@Transactional` annotation allows you to specify the desired isolation level.

Example:

```jsx
@Transactional(isolation = Isolation.REPEATABLE_READ)
public void performSomeDatabaseOperation() {
    // ...
}

```

In summary, Hibernate does not set a default isolation level by itself. It relies on the default isolation level provided by the underlying database system. You can configure the isolation level for Hibernate transactions either at the application level or on a per-transaction basis, depending on your application's requirements and the desired level of consistency and concurrency.