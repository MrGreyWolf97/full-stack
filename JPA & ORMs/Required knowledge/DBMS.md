A database management system (DBMS) is a software system for creating and managing databases.
A DBMS enables end users to create, protect, read, update and delete data in a database.
It also manages security, data integrity and concurrency for databases.

The most prevalent type of [data management](https://www.techtarget.com/searchdatamanagement/definition/data-management) platform, the DBMS essentially serves as an interface between databases and users or application programs, ensuring that data is consistently organized and remains easily accessible.

---
## What does a DBMS do?

A DBMS manages the data.
The database engine enables data to be accessed, locked and modified and the database [schema](https://www.techtarget.com/searchdatamanagement/definition/schema) defines the database's logical structure. These three foundational data elements help provide concurrency, security, [data integrity](https://www.techtarget.com/searchdatacenter/definition/integrity) and uniform data administration procedures.

> [!example] DBMS functions
> - **Administration tasks** 
>   A DBMS supports many typical database administration tasks, including [change management](https://www.techtarget.com/searchcio/definition/change-management), performance monitoring and tuning, security, and backup and recovery.
>   Most database management systems are also responsible for automated rollbacks and restarts as well as logging and auditing of activity in databases and the applications that access them.
> 
> - **Storage** 
>   A DBMS provides efficient data storage and retrieval by ensuring that data is stored in tables, rows and columns.
> 
> - **Concurrency control** 
>   In environments where multiple users access and modify the database simultaneously, a DBMS guarantees controlled transaction execution to prevent data corruption or inconsistency.
> 
> - **Centralized view** 
>   A DBMS provides a centralized view of data that multiple users can access from multiple locations in a controlled manner.
>   A DBMS can limit what data end users see and how they view the data, providing many views of a single [database schema](https://www.theserverside.com/tip/The-3-level-DBMS-schema-architecture).
>   End users and software programs are free from having to understand where the data is physically located or on what type of storage medium it resides because the DBMS handles all requests.
> 
> - **Data manipulation** 
>   A DBMS ensures data integrity and consistency by letting users insert, update, delete and modify data inside a database.
> 
> - **Data independence** 
>   A DBMS offers both logical and physical data independence to protect users and applications from having to know where data is stored or from being concerned about changes to the physical structure of data. As long as programs use the application programming interface ([API](https://www.techtarget.com/searchapparchitecture/definition/application-program-interface-API)) for the database that the DBMS provides, developers won't have to modify programs just because changes have been made to the database.
> 
> - **Backup and recovery** 
>   A DBMS facilitates backup and recovery options by creating backup copies so that data can be restored to a consistent state. This protects against data loss due to hardware failures, software errors or other unforeseen events. In a relational database management system ([RDBMS](https://www.techtarget.com/searchdatamanagement/definition/RDBMS-relational-database-management-system)) -- the most widely used type of DBMS -- the API is structured query language ([SQL](https://www.techtarget.com/searchdatamanagement/definition/SQL)), a standard programming language for defining, protecting and accessing data.

---
## What are the components of a DBMS?

A DBMS is a sophisticated piece of system software consisting of multiple integrated components that deliver a consistent, managed environment for creating, accessing and modifying data in databases.

These components include the following:

- **Storage engine**
  This basic element of a DBMS is used to store data.
  The DBMS must interface with a file system at the operating system ([OS](https://www.techtarget.com/whatis/definition/operating-system-OS)) level to store data. It can use additional components to store data or interface with the actual data at the file system level.

- **Metadata catalog**
  Sometimes called a _system catalog_ or _database dictionary_, a [metadata catalog](https://www.techtarget.com/searchdatamanagement/definition/data-catalog) functions as a repository for all the database objects that have been created.
  When databases and other objects are created, the DBMS automatically [registers information about them in the metadata catalog](https://www.techtarget.com/searchdatamanagement/feature/How-automated-metadata-management-improves-business-insights).
  The DBMS uses this catalog to verify user requests for data, and users can query the catalog for information about the database structures that exist in the DBMS.
  The metadata catalog can include information about database objects, schemas, programs, security, performance, communication and other environmental details about the databases it manages.

- **Database access language**
  The DBMS must also provide an API to access the data, typically in the form of a ==database access language== that can be used to modify data but also create database objects and secure and authorize access to the data.
  SQL is an example of a database access language and encompasses several sets of commands, including data control language for authorizing data access, data definition language for defining database structures and data manipulation language for reading and modifying data.

- **Optimization engine**
  A DBMS can also provide an optimization engine that's used to parse database access language requests and turn them into actionable commands for accessing and modifying data.

- **Query processor**
  After a query is optimized, the DBMS must provide a way to run the query and return results.

- **Lock manager**
  This crucial component of the DBMS manages concurrent access to the same data.
  Locks are required to ensure multiple users aren't trying to modify the same data simultaneously.

- **Log manager**
  The DBMS records all changes made to data managed by the DBMS.
  The record of changes is known as the log, and the log manager component of the DBMS is used to ensure that log records are made efficiently and accurately.
  The DBMS uses the log manager during shutdown and startup to ensure data integrity, and it interfaces with database utilities to create backups and run recoveries.

- **Data utilities**
  A DBMS also provides a set of utilities for managing and controlling database activities.
  Examples of database utilities include reorganization, RUNSTATS, backup and copy, recover, integrity check, load data, unload data and repair database.

- **Reporting and monitoring tools**
  Most DBMSes are integrated with reporting and monitoring tools to offer enhanced functionality for managing and analyzing data.
  Reporting tools generate reports, whereas monitoring tools track various database metrics, such as resource consumption and user activity.

![A chart showing a DBMS system and its components.](https://cdn.ttgtmedia.com/rms/onlineimages/sqlserver-dbms_components-h_half_column_mobile.png)

---
## Popular types and examples of DBMS technologies

#### RDBMS (SQL DBMS)
Sometimes referred to as a SQL DBMS and adaptable to most use cases, an RDBMS presents data as rows in tables with a fixed schema and relationships defined by values in key columns.
RDBMS [tier-1](https://www.techtarget.com/searchitchannel/definition/tier-1-vendor) products can be quite expensive, but there are high-quality, open source options, such as PostgreSQL, that can be cost-effective.

Other examples of RDBMS products include IBM Db2, [Microsoft SQL Server](https://www.techtarget.com/searchdatamanagement/definition/SQL-Server), [MySQL](https://www.techtarget.com/searchoracle/definition/MySQL), Oracle and [SingleStore DB](https://www.techtarget.com/searchdatamanagement/news/366555756/SingleStore-unveils-features-aimed-at-enabling-real-time-AI) which is a cloud-native database designed for data-intensive applications, such as [artificial intelligence](https://www.techtarget.com/searchenterpriseai/definition/AI-Artificial-Intelligence) and [machine learning](https://www.techtarget.com/searchenterpriseai/definition/machine-learning-ML)-powered applications and operational analytics.

#### NoSQL DBMS
Well-suited for loosely defined data structures that evolve over time, [NoSQL](https://www.techtarget.com/searchdatamanagement/definition/NoSQL-Not-Only-SQL) DBMSes can require more application involvement for schema management. There are four types of NoSQL database systems: document databases, [graph databases](https://www.techtarget.com/whatis/definition/graph-database), key-value stores and wide-column stores. Each uses a different type of data model, resulting in significant [differences between each NoSQL type](https://www.techtarget.com/searchcloudcomputing/tip/Compare-NoSQL-database-types-in-the-cloud).

- Document databases store semi-structured data and descriptions of that data in document format, usually [JavaScript Object Notation](https://www.theserverside.com/definition/JSON-Javascript-Object-Notation). They're useful for flexible schema requirements, such as those common with content management and mobile applications. Examples of document databases include MongoDB and Couchbase.
- Graph databases organize data as nodes and relationships instead of tables or documents. Because it stores the relationship between nodes, the graph system can support richer representations of data relationships. The graph data model doesn't rely on a strict schema and it can evolve. Graph databases are useful for applications that map relationships, such as social media platforms, reservation systems or customer relationship management. Neo4j is an example of a graph database.
- Key-value stores are based on a simple data model that pairs a unique key with an associated value. Due to this simplicity, key-value stores can be used to develop highly scalable and performant applications such as those for session management and caching in web applications or for managing shopping cart details for online buyers. Key-value databases include Redis and Memcached.
- Wide-column stores use the familiar tables, columns and rows of RDBMSes, but column names and formatting can differ from row to row in a single table. Each column is also stored separately on disk. As opposed to traditional row-orientated storage, a wide-column store is optimal when querying data by columns, such as in recommendation engines, catalogs, fraud detection and event logging. Apache Cassandra and Apache HBase are examples of wide-column stores.

#### NewSQL DBMS
NewSQL database systems are modern relational systems that use SQL and offer the same scalable performance as NoSQL systems. But NewSQL systems also provide ACID ([atomicity, consistency, isolation and durability](https://www.techtarget.com/searchdatamanagement/definition/ACID)) support for data consistency. A NewSQL DBMS is engineered as a relational, SQL database system with a distributed, fault-tolerant architecture. Other typical features of NewSQL system offerings include in-memory capability and clustered database services with the ability to be deployed in the cloud. Many NewSQL DBMS packages have fewer features and components and a smaller footprint than legacy relational offerings, making them easier to support and understand.

Some vendors now eschew the NewSQL label and describe their technologies as distributed SQL databases. CockroachDB, Google Cloud Spanner, NuoDB, Volt Active Data and YugabyteDB are examples of database systems in this category.

#### In-memory DBMS
An in-memory database management system predominantly relies on [main memory](https://www.techtarget.com/searchstorage/definition/primary-storage) for data [storage](https://www.techtarget.com/searchstorage/definition/storage), management and manipulation. By reducing the latency associated with reading from disk, an IMDBMS can provide faster response times and better performance but can consume more resources. Therefore, an in-memory database is ideal for applications that require high performance and rapid access to data, such as data stores that support real-time hybrid transactional and analytical processing (HTAP). Any type of DBMS can also support in-memory processing. SAP HANA and Redis are examples of in-memory database systems.

#### Columnar DBMS
A columnar database management system stores data in tables focused on columns instead of rows, resulting in more efficient data access when only a subset of columns is required. It's well-suited for [data warehouses](https://www.techtarget.com/searchdatamanagement/definition/data-warehouse) that have a large number of similar data items. Columnar database products include Snowflake and Amazon Redshift.

#### Multimodel DBMS
This system supports more than one database model. Users can choose the model most appropriate for their application requirements without having to switch to a different DBMS. For example, IBM Db2 is a relational DBMS, but it also offers a columnar option. Many database systems similarly qualify as multimodel through add-ons, including Oracle, PostgreSQL and MongoDB. Other products, such as Microsoft Azure Cosmos DB and MarkLogic, were developed specifically as multimodel databases.

#### Cloud DBMS
Built-in and accessed through the cloud**,** this type of DBMS can be any type -- including relational or NoSQL -- and a conventional system that's deployed and managed by a user organization or a managed service provided by the database vendor. Cloud services that enable [cloud database](https://www.techtarget.com/searchcloudcomputing/definition/cloud-database) executions include [Microsoft Azure, Google Cloud and AWS](https://www.techtarget.com/searchdatamanagement/tip/Cloud-database-comparison-AWS-Microsoft-Google-and-Oracle).

---
## Benefits of using a DBMS

A DBMS offers several key advantages over traditional file-based systems, including the following:

- **Data integrity and concurrency** 
  One of the biggest advantages of using a DBMS is that it lets users and application programmers access and use the same data concurrently while managing data integrity. Data is better protected and maintained when shared using a DBMS instead of creating new iterations of the same data stored in new files for every new application.

- **Central storage**
  A DBMS provides a central store of data that multiple users can access in a controlled manner. Central storage and management of data within the DBMS provide the following:
	- Data abstraction and independence
    - [Data security](https://www.techtarget.com/searchsecurity/feature/Top-7-types-of-data-security-technology).
    - Locking mechanism for concurrent access.
    - An efficient handler to balance the needs of multiple applications using the same data.
    - The ability to swiftly recover from crashes and errors.
    - Strong data integrity capabilities.
    - Logging and auditing of activity.
    - Simple access using a standard API.
    - Uniform administration procedures for data.

- **Data sharing and redundancy**
  A DBMS enables efficient sharing between multiple users and applications. Its capability of centralized storage also reduces data redundancy which typically occurs if the same data is stored unnecessarily in multiple locations.
  
- **Logical and structural organization of data**
  Database administrators ([DBAs](https://www.techtarget.com/searchdatamanagement/definition/database-administrator)) can use a DBMS to impose a logical, structured organization on the data. It delivers economy of scale for processing large amounts of data because it's optimized for such operations.
  
- **Data backup and recovery**
  With a DBMS, users are spared the hassle of routinely backing up data as it handles backup and recovery automatically. A DBMS restores a database to its initial state in case of a server crash or other system malfunction.
  
- **Multiple views**
  A DBMS can also provide many views of a single database schema. A view defines what data the user sees and how they see the data. The DBMS provides a level of abstraction between the conceptual schema that defines the logical structure of the database and the physical schema that describes the files, indexes and other physical mechanisms the database uses.
  
- **System modification**
  A DBMS lets users modify systems much more easily when business requirements change. A DBA can add new categories of data to the database without disrupting the existing system, thereby insulating applications from how data is structured and stored.

However, a DBMS must perform additional work to provide these advantages, thereby incurring overhead. A DBMS uses more memory and CPU than a simple file storage system, and different types of DBMSes require different types and levels of system resources.

---
## Drawbacks of DBMSes

A DBMS offers numerous advantages, but it also comes with the following drawbacks:

- **High investment and maintenance costs**
  Perhaps the single biggest drawback is the cost of the hardware, software and personnel required to run an enterprise DBMS, such as SQL Server, Oracle or IBM Db2. The hardware is usually a high-end server with a significant amount of memory configured, coupled with large disk arrays to store the data. The software includes the DBMS itself, which is pricey, as well as tools for programming and testing and for DBAs to enable management, tuning and administration. A DBMS also incurs ongoing annual maintenance costs, which increase an organization's overall investment.
  
- **Expertise requirement**
  From a personnel perspective, using a DBMS requires hiring a DBA and staff, training developers in the proper usage of the DBMS, and possibly hiring additional systems programmers to manage the installation and [integrate the DBMS into the IT infrastructure](https://www.techtarget.com/searchdatamanagement/feature/5-data-integration-challenges-and-how-to-overcome-them).
  
- **Complexity**
  DBMS software is complex and requires in-depth knowledge to properly set up and manage. But the DBMS interfaces with many other IT components, such as the OS, transaction processing systems, programming languages and networking software. Ensuring the proper configuration and efficiency of such a complicated setup can be difficult and cause performance slowdowns or even system outages.
  
- **Security vulnerabilities**
  The centralized nature of a DBMS can increase security vulnerabilities because if a single component encounters problems, it can lead to problems or even a shutdown of the entire database system. This poses a major drawback for companies that completely rely on databases.

Some of the cost and administrative overhead of running enterprise database systems can be alleviated by the cloud computing model. For example, the cloud service provider (CSP) installs and manages the hardware, which can be shared across cloud users. Furthermore, storage, memory and other resources can be scaled up and down as required based on usage needs. 
Basic DBA tasks, such as patching and simple backups, become the responsibility of the CSP.
Therefore, it can be easier and more cost-effective for some [databases to be deployed in the cloud instead of on-premises](https://www.techtarget.com/searchdatamanagement/feature/Should-you-host-your-database-on-site-or-in-the-cloud).

---
## DBMS use cases

Enterprises that need to store data and access it later to conduct business have a viable use case for deploying a DBMS. Any application requiring a large amount of data that needs to be accessed by multiple users or customers is a candidate for using a DBMS. Most medium to large organizations can benefit from using a DBMS because they have more data-sharing and concurrency needs and can more readily overcome cost and complexity issues.

Examples of customer use cases for DBMS technology include the following:

- Applications can include storing customer and account information, tracking account transactions such as withdrawals and deposits, and tracking loan payments. ATMs are a good example of a banking system that relies on a DBMS to track and manage that activity.
- DBMSes manage sales for any type of business, including storing product, customer and salesperson information and recording the sale, tracking fulfillment and maintaining sales history information.
- Most commercial airlines rely on a DBMS for data-intensive applications, such as scheduling flight plans and managing customer flight reservations.
- Manufacturing companies depend on a DBMS to track and manage inventory in warehouses. A DBMS can also be used to manage data for supply chain management applications that track the flow of goods and services, including the movement and storage of raw materials, work-in-process inventory and finished goods from the point of origin to the point of consumption.
- A DBMS makes it easier for a company to track and manage employee information in a human resources management application, including managing employee data such as addresses, phone numbers, salary details, payroll and paycheck generation.
- In educational settings, DBMSes are used to manage student records, grades and academic information, making it easier to compute averages and produce report cards.
- Healthcare systems heavily rely on DBMSes to efficiently manage and store large patient data, including [electronic health records](https://www.techtarget.com/searchhealthit/definition/electronic-health-record-EHR) that contain patient demographics, medical history and treatment plans.

---
## Changes in how DBMSes are built, sold and serviced

The landscape of DBMSes has evolved significantly in recent years, affecting how they're built, sold and serviced. The following are some major points and trends in DBMSes:

- By 2019, [open source DBMS technologies](https://www.techtarget.com/searchdatamanagement/feature/Open-source-database-comparison-to-choose-the-right-tool) were rapidly gaining traction. Gartner projected that open source databases would account for 10% of total spending on database software for that year due to increased enterprise adoption. By 2022, three of the top five databases [ranked](https://db-engines.com/en/) by DB-Engines were open source. Most mainstream IT organizations use open source software in some of their mission-critical operations. This trend complements two others: acquisitions of open source database vendors by bigger rivals and the expansion of the cloud-based database service market.
- According to Gartner, global end-user spending on database management systems is expected to expand at a 16.8% compound annual growth rate between 2022 and 2027, reaching 203.6 billion in current U.S. dollars.
- Another growing trend is what Gartner refers to as HTAP -- using a single DBMS to deliver both transaction processing and analytics without requiring a separate DBMS for each operation. To support this trend, more DBMS vendors are creating hybrid database systems that deliver multiple database engines within a single DBMS. Most hybrid DBMSes provide a combination of relational and multiple NoSQL engines and APIs. Altibase is an example of a hybrid option, whereas DataStax Enterprise is an example of a distributed hybrid database.
- Cloud DBMSes have become increasingly popular, offering the flexibility of being built in and accessed through the cloud. They can be of any type, such as relational or NoSQL, and are often deployed and managed by a user organization or a managed service provided by the database vendor.

---
## History of database management systems

The first DBMS was developed in the early 1960s when Charles Bachman created a navigational DBMS known as the Integrated Data Store. In 1968, IBM developed Information Management System or [IMS](https://www.techtarget.com/searchdatacenter/definition/IMS-Information-Management-System), a hierarchical DBMS designed for IBM mainframes that's still used today by many large organizations.

The next major advancement came in 1971 when the Conference/Committee on Data Systems Languages ([CODASYL](https://nvlpubs.nist.gov/nistpubs/Legacy/hb/nbshandbook113.pdf)) standard was delivered. Integrated Database Management System is a commercial execution of the network model database approach advanced by CODASYL.

But the DBMS market changed forever as the relational model for data gained popularity. Introduced by Edgar Codd of IBM in 1970 in [his seminal paper](http://www.morganslibrary.net/files/codd-1970.pdf) "A Relational Model of Data for Large Shared Data Banks," the RDBMS soon became the industry standard. The first RDBMS was Ingres, developed at the University of California, Berkeley by a team led by Michael Stonebraker in the mid-1970s. At about the same time, IBM was working on its System R project to develop an RDBMS.

In 1979, the first successful commercial RDBMS, Oracle, was released, followed a few years later by IBM's Db2, Sybase SQL Server and many others.

In the 1990s, as object-oriented programming ([OOP](https://www.techtarget.com/searchapparchitecture/definition/object-oriented-programming-OOP)) became popular, several OOP database systems came to market, but they never gained significant market share. Later in the 1990s, the term _NoSQL_ was coined. Over the next decade, several types of new non-relational DBMS products -- including key-value, graph, document and wide-column store -- were grouped into the NoSQL category.

Today, the DBMS market is dominated by RDBMSes, but NewSQL and [NoSQL database systems](https://www.techtarget.com/searchdatamanagement/infographic/NoSQL-database-comparison-to-help-you-choose-the-right-store) continue to grow in popularity.

_Transitioning applications and their supporting databases to a hybrid cloud requires meticulous planning, testing, and continuous management and monitoring. Explore_ [_key considerations for hybrid cloud architectures_](https://www.techtarget.com/searchdatamanagement/tip/Managing-databases-in-a-hybrid-cloud-key-considerations)_._

---
##### References 
- [TechTarget](https://www.techtarget.com/searchdatamanagement/definition/database-management-system#:~:text=A%20database%20management%20system%20(DBMS)%20is%20a%20software%20system%20for,integrity%20and%20concurrency%20for%20databases.)