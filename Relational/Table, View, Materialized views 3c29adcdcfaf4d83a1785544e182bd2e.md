# Table, View, Materialized views

### **Table**

I**s the essential building block of a SQL database.**

**It is a store of data which can be updated, replaced, and most importantly queried**.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Typically, tables are organised into a *star schema* made up of dimension and fact tables.

</aside>

### **Views**

**Views** are the logical and virtual copy of a table that is created by executing a "[**SELECT query**](https://www.tutorialspoint.com/sql/sql-select-query.htm)" statement.

The [**views**](https://www.tutorialspoint.com/sql/sql-using-views.htm) are not stored anywhere on the disk.

Thus, every time, a query has to be executed when certain data is required. But, the query expression is stored on the disk.

Views do not have a storage/update cost associated with it.

There is a SQL standard to define a view.

Views are used when data has to be accessed infrequently, but data gets updated frequently.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> With the help of Views of a table we can restrict any user to access only that data which is supposed to be accessed by him.

</aside>

### Materialized views

Materialized views are  ***virtual tables created from an editable SQL query***, whose contents are computed and stored.

Materialized views are also a logical virtual table, but in this case the result of the query is stored in the table or the disk.

The performance of the materialized views is better than normal views. This is because the data is stored on the disk.

Sometimes, materialized views are *also called "indexed views"* because the table created after the query is indexed and can be accessed faster and efficiently.

**There is not a SQL standard do define a Materialized view.**

Materialized Views are used when data is to be accessed frequently and data in table do not get updated on frequent basis.

---

<aside>
💡 *Tables* and *materialized views* are methods of organising data in SQL with different use cases.

Materialized views and tables both store data but they are fundamentally different objects in SQL.

- A materialized view is built on top of existing tables, whilst a table is the original data storage object that is used.
- A **materialized view** is *self updating* whenever the underlying tables change, whilst to update a table a job has to be run to append or replace the data.
</aside>