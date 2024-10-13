# Transactions

In a database context, a transaction is a sequence of one or more operations (SQL statements, for example) that are executed as a single unit of work. The concept of transactions is closely tied to the ACID properties, ensuring the reliability and integrity of the database despite system failures or concurrent access by multiple users.

Here's an overview of how transactions work in a database:

1. **Transaction States:**
    - **Active:** The transaction is in progress and executing its operations.
    - **Partially Committed:** All the transaction's operations have been executed, and the database is about to be updated permanently.
    - **Committed:** The changes made by the transaction are permanently saved in the database.
    - **Failed:** An error occurred during the execution of the transaction, and it cannot be completed.
    - **Aborted:** The transaction is rolled back to its initial state, undoing any changes that were made.
2. **ACID Properties:**
    - **Atomicity:** All or nothing. If any part of the transaction fails, the entire transaction is rolled back, and the database is left unchanged.
    - **Consistency:** The transaction brings the database from one valid state to another, maintaining the integrity constraints.
    - **Isolation:** Transactions can run concurrently without interfering with each other. Each transaction appears to be executed in isolation from others.
    - **Durability:** Once a transaction is committed, its changes are permanent and survive system failures.
3. **Transaction Control Statements:**
    - `BEGIN TRANSACTION:` Marks the beginning of a transaction.
    - `COMMIT:` Marks the successful end of a transaction, making its changes permanent.
    - `ROLLBACK:` Rolls back a transaction to its starting point, undoing any changes made during the transaction.
    - `SAVEPOINT:` Creates a point within a transaction to which you can later roll back.
4. **Example using SQL (PostgreSQL):**
    
    ```sql
    BEGIN; -- Start a transaction
    
    -- SQL statements (e.g., INSERT, UPDATE, DELETE)
    UPDATE accounts SET balance = balance - 100 WHERE account_id = 123;
    UPDATE accounts SET balance = balance + 100 WHERE account_id = 456;
    
    COMMIT; -- Commit the transaction
    
    ```
    
    If an error occurs between `BEGIN` and `COMMIT`, the changes are rolled back automatically. The database remains in a consistent state.
    
5. **Concurrency Control:**
    - **Read Uncommitted:** Transactions can read uncommitted changes made by other transactions.
    - **Read Committed:** Transactions can only read committed changes made by other transactions.
    - **Repeatable Read:** Transactions can read their own changes and uncommitted changes made by other transactions.
    - **Serializable:** Transactions appear to be executed serially, even though they may be executed concurrently.

Implementing transactions ensures that the database remains in a consistent and reliable state, even in the presence of errors, system failures, or concurrent access by multiple users. The database management system (DBMS) is responsible for managing transactions and ensuring their adherence to the ACID properties.