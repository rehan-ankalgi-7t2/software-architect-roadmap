# Normalization

> Normalization is a process in database design that organizes data in a relational database to reduce redundancy and dependency. 

The goal of normalization is to eliminate data anomalies (insertion, update, and deletion anomalies) and ensure that data is stored in an efficient, maintainable, and consistent manner. Normalization is usually applied to relations (tables) in a relational database.

The process of normalization is divided into several normal forms, each addressing specific types of data redundancy. The most common normal forms are `First Normal Form (1NF)`, `Second Normal Form (2NF)`, `Third Normal Form (3NF)`, and `Boyce-Codd Normal Form (BCNF)`.

Here's a brief overview of these normal forms:

1. **First Normal Form (1NF):**
    - Eliminate duplicate columns from the same table.
    - Create a separate table for each group of related data and identify each row with a unique column or set of columns (primary key).
    - Ensure that data within each column is atomic (indivisible).
2. **Second Normal Form (2NF):**
    - Meet the requirements of 1NF.
    - Remove partial dependencies, which occur when part of a composite primary key determines a non-prime attribute.
    - Move non-prime attributes that are dependent on only part of the primary key to a separate table.
3. **Third Normal Form (3NF):**
    - Meet the requirements of 2NF.
    - Remove transitive dependencies, which occur when a non-prime attribute is dependent on another non-prime attribute.
    - Move non-prime attributes that are dependent on other non-prime attributes to a separate table.
4. **Boyce-Codd Normal Form (BCNF):**
    - Meet the requirements of 3NF.
    - Remove dependencies on superkeys (candidate keys that are not the primary key).
    - Ensure that every non-trivial functional dependency is on a superkey.

Each higher normal form builds upon the previous ones, providing a systematic approach to designing a normalized relational database schema. The choice of normal form depends on the specific requirements and characteristics of the data.

Benefits of normalization include:

- Reduction of data redundancy.
- Improved data integrity.
- Simplified data maintenance.
- Better query performance in some cases.

However, normalization also has trade-offs, such as potentially increased query complexity and the need for joins in certain situations. It's essential to strike a balance between normalization and denormalization based on the specific needs of the application.