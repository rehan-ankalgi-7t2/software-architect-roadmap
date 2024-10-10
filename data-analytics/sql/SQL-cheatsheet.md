Here's a comprehensive MySQL cheat sheet to help you with common commands, functions, and best practices for working with MySQL databases.

## **Basic Commands**

- **Connect to MySQL:**
    
    ```
    mysql -u username -p
    
    ```
    
- **Create Database:**
    
    ```sql
    CREATE DATABASE database_name;
    
    ```
    
- **Select Database:**
    
    ```sql
    USE database_name;
    
    ```
    
- **Show Databases:**
    
    ```sql
    SHOW DATABASES;
    
    ```
    
- **Show Tables:**
    
    ```sql
    SHOW TABLES;
    
    ```
    
- **Describe Table Structure:**
    
    ```sql
    DESCRIBE table_name;
    
    ```
    

## **Table Management**

- **Create Table:**
    
    ```sql
    CREATE TABLE table_name (
      column1 datatype constraints,
      column2 datatype constraints,
      ...
    );
    
    ```
    
- **Drop Table:**
    
    ```sql
    DROP TABLE table_name;
    
    ```
    
- **Rename Table:**
    
    ```sql
    RENAME TABLE old_name TO new_name;
    
    ```
    
- **Add Column:**
    
    ```sql
    ALTER TABLE table_name ADD column_name datatype;
    
    ```
    
- **Drop Column:**
    
    ```sql
    ALTER TABLE table_name DROP COLUMN column_name;
    
    ```
    
- **Modify Column:**
    
    ```sql
    ALTER TABLE table_name MODIFY COLUMN column_name datatype;
    
    ```
    

## **Basic Data Operations**

- **Insert Data:**
    
    ```sql
    INSERT INTO table_name (column1, column2, ...)
    VALUES (value1, value2, ...);
    
    ```
    
- **Update Data:**
    
    ```sql
    UPDATE table_name
    SET column1 = value1, column2 = value2, ...
    WHERE condition;
    
    ```
    
- **Delete Data:**
    
    ```sql
    DELETE FROM table_name WHERE condition;
    
    ```
    
- **Select Data:**
    
    ```sql
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition
    ORDER BY column ASC|DESC
    LIMIT number;
    
    ```
    

## **Joins**
![alt text](weld.png)

- **Inner Join:**
    
    ```sql
    SELECT columns
    FROM table1
    INNER JOIN table2
    ON table1.column = table2.column;
    
    ```
    
- **Left Join:**
    
    ```sql
    SELECT columns
    FROM table1
    LEFT JOIN table2
    ON table1.column = table2.column;
    
    ```
    
- **Right Join:**
    
    ```sql
    SELECT columns
    FROM table1
    RIGHT JOIN table2
    ON table1.column = table2.column;
    
    ```
    
- **Full Join:**
MySQL does not support FULL JOIN directly, but you can achieve it using UNION:
    
    ```sql
    SELECT columns
    FROM table1
    LEFT JOIN table2
    ON table1.column = table2.column
    UNION
    SELECT columns
    FROM table1
    RIGHT JOIN table2
    ON table1.column = table2.column;
    
    ```
    

## **Indexing**

- **Create Index:**
    
    ```sql
    CREATE INDEX index_name ON table_name (column_name);
    
    ```
    
- **Create Unique Index:**
    
    ```sql
    CREATE UNIQUE INDEX index_name ON table_name (column_name);
    
    ```
    
- **Drop Index:**
    
    ```sql
    DROP INDEX index_name ON table_name;
    
    ```
    

## **Constraints**

- **Primary Key:**
    
    ```sql
    CREATE TABLE table_name (
      column_name datatype PRIMARY KEY
    );
    
    ```
    
- **Foreign Key:**
    
    ```sql
    CREATE TABLE table_name (
      column_name datatype,
      FOREIGN KEY (column_name) REFERENCES other_table(column_name)
    );
    
    ```
    
- **Unique:**
    
    ```sql
    CREATE TABLE table_name (
      column_name datatype UNIQUE
    );
    
    ```
    
- **Not Null:**
    
    ```sql
    CREATE TABLE table_name (
      column_name datatype NOT NULL
    );
    
    ```
    
- **Check:**
    
    ```sql
    CREATE TABLE table_name (
      column_name datatype,
      CHECK (condition)
    );
    
    ```
    

## **Functions**

- **String Functions:**
    
    ```sql
    SELECT CONCAT(str1, str2);
    SELECT LOWER(str);
    SELECT UPPER(str);
    SELECT LENGTH(str);
    SELECT SUBSTRING(str, start, length);
    
    ```
    
- **Numeric Functions:**
    
    ```sql
    SELECT ROUND(number, decimals);
    SELECT CEIL(number);
    SELECT FLOOR(number);
    SELECT ABS(number);
    SELECT POWER(number, exponent);
    
    ```
    
- **Date and Time Functions:**
    
    ```sql
    SELECT NOW();
    SELECT CURDATE();
    SELECT CURTIME();
    SELECT DATE_ADD(date, INTERVAL value unit);
    SELECT DATEDIFF(date1, date2);
    SELECT DATE_FORMAT(date, format);
    
    ```
    

## **Aggregation Functions**

- **Count:**
    
    ```sql
    SELECT COUNT(column) FROM table_name;
    
    ```
    
- **Sum:**
    
    ```sql
    SELECT SUM(column) FROM table_name;
    
    ```
    
- **Average:**
    
    ```sql
    SELECT AVG(column) FROM table_name;
    
    ```
    
- **Min:**
    
    ```sql
    SELECT MIN(column) FROM table_name;
    
    ```
    
- **Max:**
    
    ```sql
    SELECT MAX(column) FROM table_name;
    
    ```
    

## **Grouping and Filtering**

- **Group By:**
    
    ```sql
    SELECT column1, COUNT(column2)
    FROM table_name
    GROUP BY column1;
    
    ```
    
- **Having:**
    
    ```sql
    SELECT column1, COUNT(column2)
    FROM table_name
    GROUP BY column1
    HAVING COUNT(column2) > value;
    
    ```
    

## **Transactions**

- **Start Transaction:**
    
    ```sql
    START TRANSACTION;
    
    ```
    
- **Commit Transaction:**
    
    ```sql
    COMMIT;
    
    ```
    
- **Rollback Transaction:**
    
    ```sql
    ROLLBACK;
    
    ```
    

## **User Management**

- **Create User:**
    
    ```sql
    CREATE USER 'username'@'host' IDENTIFIED BY 'password';
    
    ```
    
- **Grant Privileges:**
    
    ```sql
    GRANT ALL PRIVILEGES ON database.* TO 'username'@'host';
    
    ```
    
- **Revoke Privileges:**
    
    ```sql
    REVOKE ALL PRIVILEGES ON database.* FROM 'username'@'host';
    
    ```
    
- **Drop User:**
    
    ```sql
    DROP USER 'username'@'host';
    
    ```
    

This cheat sheet covers many common SQL operations you might need when working with MySQL. Keep it handy for quick reference!