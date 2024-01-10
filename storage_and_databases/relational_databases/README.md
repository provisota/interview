# Scope

1. Relational Database Concepts:
    - A relational database is a type of database that stores and provides access to data points that are related to one
      another. It's based on the relational model, introduced by E. F. Codd.
    - In a relational database, data is organized into one or more tables, each with a unique key identifying the rows.
      Tables are also related if they each have a column of data that can be linked together.
    - The main components of a relational database are tables, rows, columns, and keys. A table is a collection of data
      entries and it consists of rows and columns. A row is a single record in a table, and a column is a set of data
      values of a particular type.

2. SQL (DML, DDL, DCL), Transactions, Indexes:
    - SQL (Structured Query Language) is a standard language for managing and manipulating databases. It can be divided
      into:
        - DML (Data Manipulation Language): These SQL commands are used for manipulating data. Typical operations are
          INSERT, UPDATE and DELETE.
        - DDL (Data Definition Language): These SQL commands are used for defining and modifying database schema.
          Typical operations are CREATE, ALTER and DROP.
        - DCL (Data Control Language): These SQL commands are used for controlling access to data stored in a database.
          GRANT and REVOKE are examples.
    - Transactions: A transaction is a single logical unit of work that accesses and possibly modifies the contents of a
      database. Transactions access data using read and write operations.
    - Indexes: An index is a data structure that improves the speed of data retrieval operations on a database table.
      Indexes are used to quickly locate data without having to search every row in a database table each time a
      database table is accessed.

3. Isolation Levels, Window Functions:
    - Isolation Levels: These define how and when the changes made by one operation become visible to other concurrent
      operations. Isolation levels include READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, and SERIALIZABLE.
    - Window Functions: These perform a calculation across a set of table rows that are somehow related to the current
      row. This is comparable to the type of calculation that can be done with an aggregate function. But unlike regular
      aggregate functions, use of a window function does not cause rows to become grouped into a single output row — the
      rows retain their separate identities.

# Questions

1. Can please write simple query on two tables (joing two tables)?
2. Which types of JOINs do you know?
3. What is the difference between JOIN and UNION?
4. Note: Try to ask about areas os SQL where candidate had some experience. E.g If never worked with union, but maybe
   had experience with aggregation, sorting, etc.
5. What is data normalization and denormalization and pros and cons? (Note: In case its difficult for candidate to
   answer ask about any optimization techniques the candidate knows).
6. What is aggregation function? How to filter results returned by the aggregation function?
7. What is transaction?
8. Describe ACID transaction properties. (Note: This is pure theoretical question. If candidate does not know this
   abbreviation shift question to practical case. E.g. ask how to add record to one table and increment record count in
   another table considering it will be executed in highly concurrent environment)
9. What are indexes?
10. What are use cases for RDBMS database? (Note: In case candidate is confused try to rephrase question, e.g. when
    RDBMS may not be a good choice)
11. Which transaction isolation levels do you know? Describe which problems they solve.
12. What is Window functions and their purpose?
13. Describe indexes usecases and pros/cons?

# Answers

1. A simple SQL query to join two tables can be written as follows:

```sql
SELECT table1.column1, table2.column2
FROM table1
         JOIN table2
              ON table1.common_column = table2.common_column;
```

2. There are four types of JOINs in SQL:
    - INNER JOIN: Returns records that have matching values in both tables.
    - LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table.
    - RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table.
    - FULL (OUTER) JOIN: Returns all records when there is a match in either left or right table.

3. The difference between JOIN and UNION in SQL is that JOIN is used to combine rows from two or more tables based on a
   related column between them whereas UNION is used to combine rows from different tables that are similar in
   structure.

4. In SQL, aggregation refers to the process of performing calculations on a set of values to return a single scalar
   value. Common aggregation functions include COUNT, SUM, AVG, MAX, and MIN. Sorting in SQL is done using the ORDER BY
   clause.

5. Data normalization is the process of structuring a relational database in accordance with a series of so-called
   normal forms in order to reduce data redundancy and improve data integrity. Denormalization is the process of trying
   to improve the read performance of a database, at the expense of losing some write performance, by adding redundant
   copies of data or by grouping data.

6. An aggregation function performs a calculation on a set of values and returns a single value. For example, you can
   use the COUNT() function to return the number of items, or the AVG() function to return the average value.

7. A transaction in SQL is a single unit of work that consists of one or more operations (e.g., updating a database
   record). It is treated in a coherent and reliable way independent of other transactions.

8. ACID stands for Atomicity, Consistency, Isolation, Durability. These are a set of properties that guarantee that
   database transactions are processed reliably.

9. Indexes in SQL are used to retrieve data from the database more quickly than otherwise. They are particularly
   beneficial when you need to query large amounts of data.

10. Relational Database Management Systems (RDBMS) are used when you need to store data in a structured format, enforce
    relationships between different data items, and perform complex queries.

11. Transaction isolation levels determine how and when the changes made by one operation become visible to other
    concurrent operations. They include READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, and SERIALIZABLE.

12. Window functions in SQL are used to perform calculations across a set of rows that are related to the current row.
    They provide a way to work with data that is related to the current row.

13. Indexes in SQL are used to speed up the retrieval of data from the database. They can be particularly beneficial
    when working with large amounts of data. However, they do come with some drawbacks, such as increased storage
    requirements and potential performance issues when writing data.