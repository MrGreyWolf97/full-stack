# Hibernate vs Spring Data JPA

> [!info] Table of Contents
> ```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
>```


---
# GLOSSARY
### ORM Tool
An ORM tool is a programming strategy that maps the object to the information saved in the database.
The ORM tool internally consumes the JDBC API to interact with the database.

### JPA
A Java Persistence API i.e. JPA is itself a specification of Java that is utilized to manage, access, and persist data between the Java objects and the relational databases.
> **It is contemplated as a common approach for Object Relational Mapping i.e. ORM.** 

JPA can be recognized as a bridge between object-oriented domain prototypes and relational database systems.
JPA doesn’t conduct any operation by itself, being a specification.

### Hibernate
Hibernate is a Java framework that facilitates the growth of Java applications to interact with the database.
It is an open-source, portable, ORM (Object Relational Mapping) tool.
It enforces the specifications of JPA full from the Java Persistence API for information endurance. 

Hibernate delivers a reference performance of the Java Persistence API (JPA) that makes it a tremendous choice as an ORM tool with the advantages of flexible coupling.

### Spring Data JPA
Spring Data is a component of the Spring Framework. The purpose of the Spring Data repository abstraction is to significantly lessen the amount of boilerplate code needed to execute data access layers for multiple persistence stores. 

Spring Data JPA is not a JPA provider as it is a library or framework that enhances an extra layer of abstraction on the top of our JPA provider, such as Hibernate. As of now, you are well aware of the definition of JPA, Hibernate, and Spring Data JPA. So, finally, let’s discuss the differences between hibernate and spring data JPA.

---
# Advantages of Hibernate

#### **1. Open Source and Portable** 
Hibernate framework is open-source under the LGPL license and it is lightweight.

#### **2. Quick Performance**
In quick performance, the performance of the hibernate framework is fast because the cache is internally utilized in the framework of hibernating. There are two kinds of cache in the hibernate framework i.e. one is the first-level cache and another is the second-level cache. The first-level cache is allowed by default.

#### **3. Database Independent Query**
Hibernate Query Language i.e. HQL is the object-oriented edition of SQL. It develops database-independent queries or questions. So you do not expect to write database-specific queries. Before Hibernate, if the database is altered for the project, we are required to change or modify the SQL query as well, which directs to the maintenance crisis.

#### **4. Automatic Table Creation**
Hibernate framework delivers the facility to build the tables of the database automatically. So there is no necessity to establish tables in the database manually.

[Manual Testing Services](https://www.appsierra.com/blog/manual-testing-services) complement automated processes like Hibernate by providing human insight and validation, ensuring that the software meets the highest standards of functionality and reliability

#### **5. Simplifies Complicated Join**
Retrieving data from many tables is simple in a hibernate framework.

#### **6. Delivers Query Statistics and Database Status**
Hibernate favors the Query cache and delivers statistics about the query and the database status.

---
# **Disparity Between Spring Data JPA and Hibernate**

Hibernate is a JPA implementation, while Spring Data JPA is a JPA Data Access Abstraction as we have discussed above.

Spring Data proposes a solution to GenericDao custom implementations. 

It can further generate JPA queries on your behalf through the methodology or method name conventions.
With Spring Data, you probably utilize Hibernate, Eclipse Link, or any other JPA provider. 

A very interesting advantage is that you can control transaction boundaries declaratively. 

Spring Data JPA is not an implementation or a JPA provider; it’s hardly an abstraction used to significantly decrease the amount of boilerplate code required to enforce information or data access layers for many persistence stores.


---
***References***
- [Article](https://www.appsierra.com/blog/difference-between-hibernate-and-spring-data-jpa)
