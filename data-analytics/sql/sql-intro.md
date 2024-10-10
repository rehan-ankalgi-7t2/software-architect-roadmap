# SQL (Structured query Language)

Relational Database Management System (RDBMS) concepts form the foundation of managing structured data using tables with relationships defined by keys. Here are key concepts that are fundamental to understanding RDBMS:

### 1. **Tables and Rows**

- **Tables:** In RDBMS, data is organized into tables, which are collections of related data entries. Each table has a name and consists of columns and rows.
- **Rows (Records):** Rows (or records) represent individual data entries within a table. Each row contains data for each column defined in the table schema.

### 2. **Columns and Data Types**

- **Columns (Attributes):** Columns represent specific types of data that can be stored in each row. Each column has a name and a data type (e.g., integer, string, date).
- **Data Types:** RDBMS supports various data types such as integer, float, decimal, char, varchar, date, time, etc., which define the kind of data that can be stored in a column.

### 3. **Primary Keys**

- **Primary Key:** A primary key is a unique identifier for each row in a table. It ensures that each row can be uniquely identified and retrieved. Primary keys are typically defined when creating a table and must be unique and not null.

### 4. **Foreign Keys**

- **Foreign Key:** A foreign key is a field (or collection of fields) in one table that refers to the primary key in another table. It establishes a relationship between the two tables, enforcing referential integrity.

### 5. **Normalization**

- **Normalization:** Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves breaking down large tables into smaller ones and defining relationships between them.

### 6. **Transactions**

- **Transaction:** A transaction is a sequence of operations performed as a single unit of work. In RDBMS, transactions ensure that database operations are atomic, consistent, isolated, and durable (ACID properties).

### 7. **SQL (Structured Query Language)**

- **SQL:** SQL is the standard language used to interact with RDBMS. It provides commands for querying data (`SELECT`), modifying data (`INSERT`, `UPDATE`, `DELETE`), defining data (`CREATE TABLE`, `ALTER TABLE`), and controlling access to data (`GRANT`, `REVOKE`).

### 8. **Indexes**

- **Indexes:** Indexes are data structures that improve the speed of data retrieval operations on a database table at the cost of additional storage space and decreased write performance. They are created on columns in tables to speed up SELECT queries.

### 9. **Views**

- **Views:** Views are virtual tables created by executing a query against one or more tables. They do not store data themselves but provide a way to present data in a predefined format.

### 10. **Constraints**

- **Constraints:** Constraints enforce rules on the data in a table. Common constraints include `NOT NULL` (ensures a column cannot have a NULL value), `UNIQUE` (ensures each value in a column is unique), and `CHECK` (ensures values meet a specific condition).

### Benefits of RDBMS

- **Data Integrity:** Ensures data is accurate and consistent.
- **Data Security:** Controls access to data through permissions and authentication.
- **Scalability:** Supports scaling by adding more hardware or optimizing queries.
- **Concurrency Control:** Manages simultaneous access to data by multiple users or applications.

### Popular RDBMS Examples

- **MySQL:** Open-source RDBMS, widely used for web applications.
- **PostgreSQL:** Advanced open-source RDBMS known for its extensibility.
- **Oracle Database:** Enterprise-grade RDBMS with comprehensive features.
- **SQL Server:** Microsoft's RDBMS with strong integration with Windows environment.
- **SQLite:** Lightweight, embedded RDBMS suitable for small-scale applications.

Understanding these fundamental concepts of RDBMS is essential for designing efficient database schemas, writing optimized SQL queries, and ensuring data integrity and security in applications.

## ACID Principles 🧪

ACID is an acronym that represents a set of properties that guarantee reliable processing of database transactions. These properties ensure the consistency and integrity of transactions in a database system. The ACID properties are:

`1. Atomicity`: A transaction is either executed entirely or not at all. If any part of the transaction fails, the entire transaction is rolled back to its original state. This prevents inconsistencies in the data.
- Example: In a banking system, transferring money from one account to another must involve two steps: deducting from one account and adding to another. If one of these steps fails (e.g., due to a system crash), the whole transaction is rolled back to its original state, ensuring no partial updates are made.

`2. Consistency`: A transaction must leave the system in a consistent state. This means that all data integrity constraints are maintained. For example, if a transfer of funds from one account to another is a transaction, the total balance of both accounts should remain unchanged after the transaction is completed.
- Example: Assume you have a database where all entries in a column must be unique. During a transaction, if a new entry violates this rule, the entire transaction will fail and rollback, maintaining the consistent state of the database.

`3. Isolation`: Transactions should not interfere with each other. This means that the execution of one transaction should not affect the execution of another transaction. This is achieved through mechanisms like locking or timestamping.
- Example: If two users are concurrently updating the same row in a table, isolation ensures that one user’s changes do not interfere with the other’s until the first transaction is completed. Isolation levels (e.g., Read Committed, Serializable) control the degree of isolation.

`4. Durability`: Once a transaction is committed, its changes are made permanent and will not be lost, even if the system fails. This is typically achieved through redundancy and logging.
- Example: After a money transfer transaction is successfully completed and committed, the updated balances of both accounts should persist in the database even if the system crashes immediately after.