 > [!info] The JDBC API consists of a set of interfaces and classes written in the Java programming language.
> [Java Database Connectivity](https://www.ibm.com/docs/en/informix-servers/12.10?topic=started-what-is-jdbc) is the JavaSoft specification of a standard API that allows Java programs to access database management systems.

Using these standard interfaces and classes, programmers can write applications that connect to databases, send queries written in structured query language (SQL), and process the results.

Since JDBC is a standard specification, one Java program that uses the JDBC API can connect to any ==Database Management System== (DBMS), as long as a driver exists for that particular DBMS.

> [!success] Universal Data Access
As long as it's used Standard SQL (ANSI SQL for most of the cases) ==queries are Hot Swappable== (it's possible to swap between databases with the same characteristic), and so it's the code written server side.

---
## JDBC Driver

The JDBC API defines the Java™ interfaces and classes that programmers use to connect to databases and send queries. 

> A JDBC driver implements these interfaces and classes for a particular DBMS vendor.

A Java program that uses the JDBC API loads the specified driver for a particular DBMS before it actually connects to a database.
The JDBC **DriverManager** class then sends all JDBC API calls to the loaded driver.

> [!info] There are four types of JDBC drivers:
> 
>##### Type 1 driver - JDBC-ODBC bridge plus ODBC driver
   Translates JDBC API calls into ==Microsoft ODBC== calls that are then passed to the ODBC driver
   The ODBC binary code must be loaded on every client computer that uses this type of driver.
   ODBC is an acronym for Open Database Connectivity.
   >
>##### Type 2 driver: Native-API, partly Java driver
   Converts JDBC API calls into DBMS-specific client API calls
   Like the bridge driver, this type of driver requires that some binary code is loaded on each client computer.
   >
>##### Type 3 driver: JDBC-Net, pure-Java driver
   Sends JDBC API calls to a middle-tier server that translates the calls into the DBMS-specific network protocol
   The translated calls are then sent to a particular DBMS.
   >
>##### Type 4 driver: Native-protocol, pure-Java driver
   Converts JDBC API calls directly into the DBMS-specific network protocol without a middle tier

This driver allows the client applications to connect directly to the database server.

---
## Basic flow

![[Pasted image 20240726170457.png]]
1. The Application will *mount the driver*
2. Using the driver, the App will *create a connection*
3. Using the connection, the App will *execute SQL queries*
4. After executing the queries, the App will be able to *commit/rollback those queries*
5. In the end, the App will *close the connection*

---

## Terminology
#### Connections
- **DriverManager**: a class that interacts with the driver for creating connections. The legacy way of connecting to databases
- **DataSource**: used in systems with multiple threads operating on the database. Proveds Thread Pooling
- **Connection**: manages the actual communication between the client and the server
#### Executions
- **Statement**: representation of the SQL to be executed against the database
- **ResultSet**: response from the database in a logical "tabular" form
- **PreparedStatement**: an extension of Statement that is used for precompiled statements (with inputs). Useful for large statements that need to be compiled at runtime
- **CallableStatement**: an extension of PreparedStatement that references ==stored procedures== in the database (with inputs and outputs).

#### Transactions
Enables to have a block of code all executed together within a single commit.
- **Auto-commit**: a function of a database driver where each statement is immediately readable by all processes once executed in the RDBMS. The statement is immediately commited.
- **Transaction**: a series of statements that must be executed ==completely or not at all== before any other process can read them.
  > *It actually depends on the level of Isolation, but it's correct for the default one*
- **Rollback**: a mechanism by which all statements of a transaction are removed from the database such that it appears to all current and future processes as never having occured.
  -> **Atomicity**


---
##### References
- [IBM doc](https://www.ibm.com/docs/en/informix-servers/12.10?topic=started-what-is-jdbc)
- 