### [JPA](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad#what-is-jpa)

Have you ever wondered what enables the interaction between our Java applications and databases?
This is all made possible by the Java Persistence API. 
JPA provides and defines the specifications for persisting, accessing, and managing data between Java objects (POJO or Entity) and relational databases.

### [Hibernate](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad#what-is-hibernate)

> [!tip] Hibernate-ORM is one of the most popular ==implementations== of JPA.

Both Hibernate and JPA need each other.
Hibernate  helps to map Java objects to database tables.
What it does under the hood, is to translate Java codes into SQL queries that the DBMS (Database Management System) can understand. Let’s look at the illustration, which shows the mapping of an Entity to a Database table.

![An graphical representation of mapping an object or class entity to a relational database through Hibernate](https://miro.medium.com/v2/resize:fit:421/1*DiktbvdVxqTnd_iMIggFbQ.png)

---
### [Key differences](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad#key-differences-between-jpa-and-hibernate)

- JPA is a mere specification for managing the database.
- JPA has no implementation, as it is a guideline to follow to manipulate our database. 
- Hibernate is the implementation of the JPA specification.
  Hibernate is the code implementation that meets the API as defined by the JPA specification.
- JPA can be called the interface, while Hibernate is the implementation of these interfaces.
- JPA specifies standards for developers to perform database operations seamlessly, while Hibernate uses these standards of the Java Persistence API to carry out operations on the database.
- It is also worth knowing that JPA has its native query language called Java Persistence Query Language (JPQL), which is an object-oriented query language to perform database operations. On the other hand, Hibernate uses HQL (Hibernate Query Language), which is also an object-oriented query language to perform database operations.

---
### [Relationship between](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad#relationship-between-jpa-and-hibernate)

To maintain the relationship between the two, Hibernate must adhere to the rules made available by the JPA specification.

We can also deduce that JPA provides a standardized mechanism for Java applications to connect with a DBMS via Hibernate or any other JPA implementation

It abstracts away many of the low-level details of database administration. Let’s look at the diagram below.

Communication between JPA and Hibernate:

![Communication taking place between JPA and Hibernate](https://miro.medium.com/v2/resize:fit:700/1*S_vZOWfmkl0iZt8D7YjEUQ.png)

You can see from the basic illustration that our Java program communicates with the JPA interface.
The Hibernate implementation is communicated using the JPA interface.
Hibernate converts Java objects into SQL queries, which it then sends to the database.
The database executes the SQL queries and returns the results to Hibernate (if need be). Hibernate returns the results to your Java application in the form of Java objects.

---
##### References
- [StackCademy](https://stackademic.com/blog/understanding-the-key-differences-jpa-vs-hibernate-orm-in-java-applications-f7c56b980dad)