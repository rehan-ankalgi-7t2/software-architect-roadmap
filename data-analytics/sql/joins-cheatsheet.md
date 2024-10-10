# SQL Joins
SQL Joins explained briefly with examples. Applies to MS SQL. Assumes both tables contain unique records.
Extracted from Jeff Attwood's blog post: https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/

## Sample Data
TABLE-A

| id            | name          | 
| ------------- |:-------------:| 
| 1             | Pirate        | 
| 2             | Monkey        | 
| 3             | Ninja         | 
| 4             | Spaghetti     | 

TABLE-B

| id            | name          | 
| ------------- |:-------------:| 
| 1             | Rutabaga      | 
| 2             | Pirate        | 
| 3             | Darth Vader   | 
| 4             | Ninja         | 

## INNER JOIN (Default if only JOIN keyword is used)
All matching records from the joined tables. Memory aid: intersection in venn diagram.

```sql
SELECT * FROM TABLEA ta
INNER JOIN TABLEB tb
ON ta.name = tb.name
```
| id            | name          | id            | name          | 
| ------------- |:-------------:| ------------- |:-------------:|
| 1             | Pirate        | 2             | Pirate        | 
| 3             | Ninja         | 4             | Ninja         | 

## OUTER JOIN
### FULL OUTER JOIN
Produces the set of all records in Table A and Table B, with matching records from both sides where available. If there is no match, the missing side will contain null.

```sql
SELECT * FROM TableA
FULL OUTER JOIN TableB          
ON TableA.name = TableB.name
```

### LEFT OUTER JOIN
produces a complete set of records from Table A, with the matching records (where available) in Table B. If there is no match, the right side will contain null.
In Entity Framework, DefaultIfEmpty() method on an entity translates to a left outer join.

```sql
SELECT * FROM TableA
LEFT OUTER JOIN TableB        -- imagine this reads as left outer join A with B, so everything in A and Matching in B
ON TableA.name = TableB.name  -- if nothing matches in B, return null
```

### RIGHT OUTER JOIN
Not supported in Entity Framework, can be achived by flipping the tables being joined.

---
![](https://cooltechiedotblog.wordpress.com/wp-content/uploads/2017/04/capture6.png)