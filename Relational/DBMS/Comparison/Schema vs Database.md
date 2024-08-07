> [!info] Table of contents
>```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
>```

---
## Overview
### Database
A _database_ (often referred to as DB) is an organized structure designed to store, modify, and process related information, mostly in large volumes.

Databases are actively used for dynamic sites with significant amounts of data.
Often, these are online stores, portals, and corporate websites.
Such websites are usually developed using a server-side programming language (for example, PHP) or based on a CMS (for example, WordPress), and do not have ready-made data pages by analogy with HTML sites.

Pages of dynamic sites are formed on the fly as a result of the interaction of scripts and databases after a corresponding request from the client to the web-server.

### Schema
The term _database schema_ can mean either a visual data representation, a set of rules it is subject to, or a complete set of objects owned by a particular user.
An easy way to imagine a schema is to think of it as a field that contains tables, stored procedures, views, and related data resources.
The schema defines the infrastructure of this field.

---

## Main difference

A **==Database==** is any collection of data.
The data in a database is usually organized in such a way that the information is easily accessible.

A **==Schema==** is basically a formal description of how a database is formed and where everything is located.
It works as a blueprint that shows where everything is in the database and how it is structured.


![Database vs. Schema Comparison Table](https://blog.devart.com/wp-content/uploads/2022/05/database_schema_comparison.png)


It is important to differentiate between the logical concept of a _schema_ that exists regardless of a specific DBMS and _schema_ as a physical object.
This logical concept is synonymous with the structure or model of a database.
Now, let us look a little bit deeper into the peculiarities of ==schemas as physical objects== in different RDBMSs.

---

## Database vs. Schema

> [!info] SQL Server and PostgreSQL
> Both in SQL Server and PostgreSQL, a schema is a physical database object that stores other database objects.

#### PostgreSQL
> Database administrators can set different levels of access for different users in order to avoid conflicts and unnecessary interference.

- ***Database***: it can be defined as *==a container with all the schemas, records, logs, and table constraints==*.
  Databases are strictly separated, which means that a user cannot access two databases at once.
  Use DML (Data Manipulation Language) commands in order to manipulate data in the PostgreSQL database.

- ***Schema***: determines how the data is logically structured and stored in a database.
  It contains all the indexes, tables, functions, data types, stored procedures, and anything that might be related.


#### SQL Server
> In the context of SQL, use Data Definition Language (DDL) for creating and modifying database objects.
> In case you are looking for a better [understanding of a SQL schema](https://blog.devart.com/understanding-a-sql-schema.html), please refer to another blog article of ours.

#### Oracle
> At the same time, working with a database in Oracle is almost identical to working with SQL Server.
> Namely, users connect to an Oracle server and work with the schemas just like they do with databases in SQL Server.

- ***Database***: physical files that contain data and metadata.
  These include the datafiles, controlfiles, and redo log files.
  A _database instance_ in Oracle comprises a memory that is shared and accessed by all the threads and background processes.
  This includes the SGA, PGA, and background processes such as RECO, SMON, DBWO, PMON, CKPT, ARCO, etc.

- ***Schema****: Unlike SQL Server and PostgreSQL, there is no separate _schema_ object.
  However, if a _user_ becomes an owner of any objects like tables, views, etc., it is treated as a schema.

![](https://blog.devart.com/wp-content/uploads/2022/04/database_vs_schema_oracle_database.png)



![](https://blog.devart.com/wp-content/uploads/2022/04/database_vs_schema_oracle_instance.png)

#### MySQL
> There is no such object as schema. Sometimes, a schema is used as a synonym for a database. In MySQL syntax, you can easily substitute the `SCHEMA` keyword with the `DATABASE` keyword.
> This way, using `CREATE SCHEMA` will give you the same result as `CREATE DATABASE`.

---

***References***
- [Devart blog](https://blog.devart.com/difference-between-schema-database.html)