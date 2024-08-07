
Structured Query Language (SQL) stands as the cornerstone of modern data management and analysis, powering everything from simple data retrieval tasks to complex analytics across vast databases.

Its ubiquity across different database systems has made it one of the most valuable skills for anyone working with data.
However, with various SQL dialects in use, the question of standardization becomes paramount.

This is where ANSI SQL enters the picture, serving as a standardized benchmark that ensures a high level of compatibility and interoperability between different database systems.
This blog aims to unravel the layers of ANSI SQL, guiding you through its key components and demonstrating its critical role in today’s data-driven world.

> [!info] Table of contents
> 
>```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
>```


---
# Why ANSI SQL Matters

The American National Standards Institute (ANSI) plays a critical role in standardizing SQL, ensuring that SQL statements can, for the most part, be ==used across different database systems== without significant modification.

This standardization is crucial for several reasons:
##### **Interoperability**
ANSI SQL facilitates the exchange of data across various systems by providing a common language for databases. This means that learning ANSI SQL equips you with the ability to work across multiple database platforms, from MySQL and PostgreSQL to SQL Server and Oracle, with minimal adjustments to your query syntax.

##### **Career Advantages**
Given the widespread adoption of SQL in the data industry, proficiency in ANSI SQL opens up numerous career opportunities.
Whether you are a data analyst, database administrator, or software developer, understanding ANSI SQL enhances your versatility and marketability.

##### **Broader Applicability**
ANSI SQL’s standardization efforts have led to the inclusion of advanced features over time, such as *window functions* and *common table expressions* (CTEs), which were once proprietary extensions in certain SQL dialects.
Learning ANSI SQL means staying at the forefront of database technology, prepared to leverage its full potential for sophisticated data manipulation and analysis.

In the following sections, we will delve into the core aspects of ANSI SQL, includin:
- Data Definition Language (DDL)
- Data Manipulation Language (DML)
- Aggregations
- Joins
- Unions
- CTEs
- Window functions

Each section will provide insights into the syntax and application of these elements, illustrated with examples to enhance your understanding and skills in ANSI SQL.

---
# Data Definition Language (DDL)

The foundation of any database operation begins with its structure, and this is where Data Definition Language (DDL) plays a pivotal role. DDL allows you to define, alter, and delete database schemas, tables, views, and indexes, providing the blueprint upon which data can be stored, retrieved, and manipulated. Understanding DDL is crucial for anyone looking to work with databases, as it enables the creation of a structured environment where data can reside.

##### **CREATE**
The CREATE statement is used to establish new databases, tables, and views. For example, creating a new table involves specifying its name and defining its columns, along with their data types and constraints:
```SQL
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    position VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10, 2)
);
```
> This statement creates a table named employees with various fields such as employee_id, name, position, department, and salary, each with a specified data type.

##### **ALTER**
When the structure of an existing database entity needs modification, the ALTER statement comes into play.
It can be used to add, delete, or modify columns in a table and to change other properties:
```SQL
ALTER TABLE employees ADD COLUMN email VARCHAR(255);
```
> This example adds a new column named email to the employees table.

##### **DROP**
To remove an existing database, table, or view, the DROP statement is used. It is a powerful command that should be used with caution, as it deletes the entity and its data permanently:
```SQL
DROP TABLE temporary_data;
```
>This command removes the temporary_data table from the database.

---
##### **Indexes and Constraints**

> [!tip] In addition to basic structure definitions, DDL is also used to define indexes and constraints which are essential for ensuring data integrity and optimizing query performance.

Indexes are ==special lookup tables== that the database search engine can use to speed up data retrieval.
Creating an index on a table makes searches based on the indexed column much faster.

```SQL
CREATE INDEX idx_employee_name ON employees (name);
```
> This creates an index for the name column in the employees table.

Constraints define certain rules that the data in the database must follow.

> [!example] Common constraints
>- PRIMARY KEY
>- FOREIGN KEY
>- UNIQUE
>- NOT NULL
>- CHECK

```SQL
ALTER TABLE employees ADD CONSTRAINT unique_email UNIQUE (email);
```
> This ensures that all email addresses in the employees table are unique.

Understanding and effectively using DDL statements are fundamental skills for anyone working with databases.
They allow for the creation and modification of the database’s structure, which is crucial for storing and organizing data efficiently. 

---
# Retrieving Data

##### **SELECT**
The most frequently used statement, SELECT, retrieves data from one or more tables. It can be used to select specific columns, aggregate data, and join data from multiple tables.
```SQL
SELECT name, position, salary
FROM employees
WHERE department = 'Engineering';
```
> This retrieves the names, positions, and salaries of all employees in the Engineering department.

In the next section, we’ll explore retrieving data then how Data Manipulation Language (DML) enables us to interact with the data within these structures.

---
# Data Manipulation Language (DML)

Once the structure of a database has been defined using DDL, the next step involves interacting with the data itself.
This is where ==Data Manipulation Language== (DML) comes into play.
DML provides the necessary commands to insert, update, delete, and retrieve data from the database.
Mastery of DML commands is essential for anyone looking to work with data within SQL databases, as it enables the manipulation and retrieval of data stored within the database structures created by DDL.

##### **INSERT**
The INSERT statement is used to add new records into a table. It can insert values into all or specified columns.
```SQL
INSERT INTO employees (employee_id, name, position, department, salary)
VALUES (1, 'John Doe', 'Software Developer', 'Engineering', 75000);
```
> This statement adds a new row into the employees table with values for each of the specified columns.

##### **UPDATE**
The UPDATE statement modifies existing records in a table. It is often used in conjunction with a WHERE clause to specify which records should be updated.
```SQL
UPDATE employees
SET salary = 80000
WHERE employee_id = 1;
```
> This updates the salary of the employee with employee_id 1 to 80000.

##### **DELETE**
The DELETE statement removes existing records from a table. Similar to UPDATE, it can be used with a WHERE clause to target specific records for deletion.
```
DELETE FROM employees
WHERE employee_id = 1;
```
> This statement deletes the record of the employee with employee_id 1 from the employees table.

The power of DML lies in its ability to manipulate the data within the database’s structures effectively.
By inserting, updating, and deleting data users can manage and analyze their data to inform decision-making processes.

The next sections will delve deeper into SQL features that enable more complex data manipulation and analysis, such as aggregations, joins, and advanced functions like window functions and common table expressions (CTEs).

---
# Aggregations

Aggregations in SQL are powerful tools for summarizing and analyzing data, allowing you to perform calculations on a set of values to yield a single value.
By using aggregation functions, you can compute statistics and insights across rows that share common characteristics. Understanding these functions is essential for data analysis, reporting, and making informed decisions based on large datasets.


##### **COUNT()**
Counts the number of rows in a dataset, optionally counting only distinct values.
```SQL
SELECT COUNT(*) FROM employees;
```
> This query counts the total number of employees in the employees table.


##### **SUM()**
Calculates the total sum of a numeric column.
```SQL
SELECT SUM(salary) FROM employees WHERE department = 'Engineering';
```
>This returns the total sum of salaries for employees in the Engineering department.


##### **AVG()**
Computes the average value of a numeric column.
```SQL
SELECT AVG(salary) FROM employees;
```
> This calculates the average salary of all employees.


##### **MIN() and MAX()**
Determine the minimum and maximum values of a column.
```SQL
SELECT MIN(salary), MAX(salary) FROM employees;
```
> This query finds the lowest and highest salaries among all employees.


##### **GROUP BY**
To make aggregation more powerful, SQL provides the GROUP BY clause, which groups rows sharing a common attribute into summary rows.
This is particularly useful when you want to apply an aggregation function to each group separately.
```SQL
SELECT department, AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```
> This query calculates the average salary within each department, showcasing how GROUP BY can be used to segment data into meaningful categories.


> [!tip] Filtering Aggregated Data with HAVING
> While the WHERE clause is used to filter rows before they are grouped, the HAVING clause is used to filter groups created by GROUP BY.
> ```SQL
SELECT department, AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
>```
> >This query returns only those departments where the average salary is greater than 60,000, illustrating how HAVING complements GROUP BY by enabling conditional aggregation.

Aggregation functions are indispensable in SQL for summarizing data, allowing for complex analyses and insights into the underlying data patterns.

Whether you’re calculating simple averages or segmenting data into groups for detailed comparisons, understanding and utilizing these functions will significantly enhance your data analysis capabilities. 

The next section will explore joins, another critical aspect of SQL for combining data from multiple tables.

---
# Joins

Joins are a fundamental aspect of SQL that allow you to combine rows from two or more tables based on a related column between them.
This feature is crucial for relational databases where data is often normalized and distributed across multiple tables.
Understanding joins is essential for querying and analyzing data from these interconnected tables.

##### **INNER JOIN**
This join returns rows when there is at least one match in both tables. If there is no match, the rows are not returned.
```SQL
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.id;
```
> This query retrieves employee names along with their respective department names by matching department_id from the employees table with id in the departments table.


##### **LEFT JOIN (or LEFT OUTER JOIN)**
This join returns all rows from the left table, and the matched rows from the right table. The result is NULL from the right side if there is no match.
```SQL
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.id;
```
> Here, all employees are listed along with their department names. If an employee does not belong to a department, the department name will be NULL.


##### **RIGHT JOIN (or RIGHT OUTER JOIN)**
This join returns all rows from the right table, and the matched rows from the left table. The result is NULL from the left side if there is no match.
```SQL
SELECT employees.name, departments.department_name
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.id;
```
> This query lists all departments, including those without any employees, with employee names where applicable.



##### **FULL OUTER JOIN**
This join returns rows when there is a match in one of the tables. It effectively combines the results of both LEFT JOIN and RIGHT JOIN.
```SQL
SELECT employees.name, departments.department_name
FROM employees
FULL OUTER JOIN departments ON employees.department_id = departments.id;
```
> This retrieves all employees and all departments, with NULL values in places where there is no match.


> [!tip] Using Joins for Complex Queries
>Joins can be used to construct complex queries that involve multiple tables.
>They are particularly useful for reports that require data from different areas of a database.
>For example, to analyze the average salary by department, you might:
>1. use an INNER JOIN between the employees and departments tables
>2. group and aggregation functions
>
>```
SELECT departments.department_name, AVG(employees.salary) AS average_salary
FROM employees
INNER JOIN departments ON employees.department_id = departments.id
GROUP BY departments.department_name;
>```
>> This query demonstrates how joins can be combined with other SQL features to provide insightful data analysis.

Understanding and mastering the different types of joins is crucial for any data professional.

They enable you to navigate and manipulate the relationships between tables in a relational database, opening up a vast array of possibilities for data querying and analysis.

In the next section, we’ll explore unions, another powerful feature for combining results from multiple SQL queries.

---
# Unions

SQL unions are used to combine the results of two or more SELECT queries into a single result set.

This feature is particularly useful when you need to aggregate data from different tables that have similar structures but reside in separate parts of your database.
Understanding how to use unions effectively can significantly enhance your data analysis capabilities by allowing you to consolidate data from multiple sources.


##### **UNION**
The UNION operator is used to combine the results of two or more SELECT queries. It automatically removes duplicate rows from the result set. All SELECT statements within the UNION must have the same number of columns in the result sets with similar data types.
```SQL
SELECT name FROM employees
UNION
SELECT name FROM contractors;
```
>This query selects names from the employees table and combines them with names from the contractors table, removing any duplicates in the process.


##### **UNION ALL**
The UNION ALL operator also combines the results of two or more SELECT queries but does not remove duplicates. It is generally faster than UNION because it does not require the extra step of checking for and removing duplicate rows.
```SQL
SELECT name FROM employees
UNION ALL
SELECT name FROM contractors;
```
>Here, names from both the employees and contractors tables are combined, including duplicates.


> [!example] Practical usage
> Unions are particularly useful in scenarios where data is segmented across similar tables.
> For example, if historical data is archived in separate tables by year, unions can be used to consolidate this data for analysis.
> They are also handy for creating comprehensive reports that aggregate information from various parts of a database.

> [!tip] When Using Unions
> **Column Compatibility:** The SELECT statements being combined must have the same number of columns, and the columns must have compatible types.
>
>**Ordering and Limiting Results:** When you need to order or limit the overall result set of a union, you should use an outer SELECT statement:
>
>```SQL
SELECT * FROM (
  SELECT name FROM employees
  UNION
  SELECT name FROM contractors
) AS combined_names
ORDER BY name
LIMIT 10;
>```
>> This query combines names from employees and contractors, orders the combined list by name, and limits the results to the first 10 rows.

Unions are a powerful feature of SQL that enable the consolidation of data for analysis and reporting.

By understanding and applying UNION and UNION ALL appropriately, you can efficiently aggregate data from multiple sources, enhancing your data querying and analysis capabilities.

The next section will delve into Common Table Expressions (CTEs), another advanced SQL feature that simplifies complex queries and enhances readability.

---
## Common Table Expressions (CTE)

Common Table Expressions (CTEs) provide a way to write more readable and maintainable SQL queries by allowing you to define a temporary result set that you can reference within a SELECT, INSERT, UPDATE, or DELETE statement.

CTEs are particularly useful for breaking down complex queries into simpler parts, making them easier to understand and maintain.

> [!success] They also enable recursive queries, which are powerful for dealing with hierarchical or tree-structured data.

> [!tip] ### Simple CTE
> A CTE is defined using the WITH clause followed by the CTE name, an optional column list, and the query that defines the CTE.
> The basic syntax is as follows:
>
>```SQL
>WITH CteName (column1, column2, ...) AS (
 >   SELECT column1, column2, ...
>    FROM table_name
>    WHERE condition
>)
>SELECT * FROM CteName;
>```
>
>Let’s look at a simple example to understand how CTEs work:
>
>```SQL
>WITH DepartmentSalaries AS (
>    SELECT department_id, AVG(salary) AS average_salary
>    FROM employees
>    GROUP BY department_id
>)
>SELECT departments.department_name, DepartmentSalaries.average_salary
>FROM departments
>JOIN DepartmentSalaries ON departments.id = DepartmentSalaries.department_id;
>```
> >In this example, the CTE DepartmentSalaries calculates the average salary for each department.
> > The main query then joins this CTE with the departments table to get the department names alongside the average salaries.

> [!tip] ### Recursive CTEs
>
>Recursive CTEs are a powerful feature that allows you to perform recursive operations.
>
>They are typically used for ==querying hierarchical data==, such as organizational charts or category trees.
>
>**A recursive CTE consists of two parts:**   the anchor member (the initial query that returns the base result set) and the recursive member (the query that references the CTE and adds to the result set). The UNION or UNION ALL operator is used to combine these two parts.
>
>```SQL
>WITH RECURSIVE CteName AS (
>    -- Anchor member
>    SELECT column1, column2
>    FROM table_name
>    WHERE condition
>    UNION ALL
>    -- Recursive member
>    SELECT t.column1, t.column2
>    FROM table_name t
>    INNER JOIN CteName c ON t.parent_column = c.column1
>)
>SELECT * FROM CteName;
>```

---
### Advantages of Using CTEs
##### **Readability**
CTEs make complex queries easier to read and understand by allowing you to name and define specific parts of the query.

##### **Maintainability**
By breaking down complex queries into simpler parts, CTEs make it easier to maintain and modify your SQL code.

##### **Recursion**
Recursive CTEs provide a way to deal with complex data structures that are difficult to query with standard SQL features.

CTEs are an advanced SQL feature that can greatly enhance the clarity and functionality of your SQL queries.
Whether you’re dealing with complex joins, hierarchical data, or simply want to improve the readability of your SQL, CTEs offer a structured and powerful solution.

In the next section, we will explore window functions, another advanced feature that extends the capabilities of SQL for analytical tasks.

---
# Window Functions

Window functions are a feature of SQL that allow you to perform calculations across a set of rows that are related to the current row.

Unlike standard aggregation functions, which collapse the rows into a single output row, window functions retain the original row structure, allowing for more complex calculations and analyses. 

They are particularly useful for tasks that involve ==ranking, running totals, moving averages==, and more.

> [!example] Basic Concepts of Window Functions
>
>To use a window function, you specify the function followed by the OVER() clause, which defines the window or set of rows the function operates on.
>
>The OVER() clause can include partitioning, ordering, and framing components:
>
>1. **Partitioning:** Divides the result set into partitions to which the function is applied independently.
>
> 2. **Ordering:** Orders the rows within each partition. Framing: Specifies the subset of rows within the partition to be considered for each row’s calculation.



##### **Ranking functions**
Such as ROW_NUMBER(), RANK(), DENSE_RANK(), and NTILE(), are used for assigning ranks to rows within a partition.
```SQL
SELECT name,
	salary, 
    ROW_NUMBER() OVER (ORDER BY salary DESC) as rank
FROM employees;
```
> This query assigns a unique rank to each employee based on their salary, with the highest salary receiving a rank of 1.


##### **Analytic functions**
Such as LEAD(), LAG(), FIRST_VALUE(), LAST_VALUE(), allow for comparisons between rows within a partition.
```SQL
SELECT name, 
	salary, 
    LEAD(salary) OVER (ORDER BY salary DESC) as next_higher_salary
FROM employees;
```
> This returns each employee’s salary and the salary of the next higher-paid employee.


##### **Aggregate functions**
Standard aggregate functions like SUM(), AVG(), MIN(), MAX() can also be used as window functions with the OVER() clause.
```SQL
SELECT name, department_id, salary,
       SUM(salary) OVER (PARTITION BY department_id) as department_salary_total
FROM employees;
```
> This query shows each employee’s salary along with the total salary for their department.


> [!example] Practical Uses of Window Functions
>
>Window functions are invaluable for data analysis, allowing for sophisticated calculations that are difficult or impossible to perform with standard SQL aggregates or joins.
>
>For example, they can be used to:
>
>- Calculate running totals and moving averages.
>- Perform row-by-row comparisons, such as finding the difference in sales from one month to the next.
>- Rank items within categories, such as finding the top 3 best-selling products in each category.
>
>Window functions extend the analytical capabilities of SQL, enabling more dynamic and complex analyses directly within your database queries.

By understanding and applying these functions, you can unlock deeper insights into your data, making it easier to perform sophisticated data analysis tasks without resorting to external processing tools.

With the power of window functions, SQL continues to be an indispensable tool for data analysts and database professionals alike.
# ---
##### References
- [LinkedIn Article](https://www.linkedin.com/pulse/ansi-sql-101-understanding-syntax-concepts-alex-merced-wswye/)