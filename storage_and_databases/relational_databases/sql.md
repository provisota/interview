# Relational Database SQL

SQL (Structured Query Language) is a standard language for storing, manipulating, and retrieving data in relational
databases. It is widely used for its ability to handle structured data, where data is organized in tables.

- **Key Operations**: SQL operations include `SELECT` (retrieve data), `INSERT` (add new data), `UPDATE` (modify
  existing data), and `DELETE` (remove data).
- **Querying**: SQL allows for complex querying to retrieve specific data by joining tables, filtering records, and
  aggregating data.
- **Data Definition Language (DDL)**: Used to define and modify database schema through commands
  like `CREATE TABLE`, `ALTER TABLE`, and `DROP TABLE`.
- **Data Manipulation Language (DML)**: Used for data manipulation, including inserting, updating, and deleting records.
- **Data Control Language (DCL)**: Manages access to data using commands like `GRANT` and `REVOKE`.
- **Transactional Control**: Provides transactional control commands like `BEGIN TRANSACTION`, `COMMIT`, and `ROLLBACK`
  for maintaining data consistency.

## Q&A

### How does SQL ensure data integrity and consistency in database operations?

**SQL ensures data integrity and consistency through various mechanisms:

- **Constraints**: SQL allows defining constraints like `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, and `CHECK`
  to enforce data integrity rules.
- **Transactions**: SQL supports transactional control, which ensures that a group of SQL operations either all succeed
  or fail as a unit. This atomicity, along with features like `COMMIT` and `ROLLBACK`, helps in maintaining consistency.
- **Referential Integrity**: The use of foreign keys in SQL enforces referential integrity, ensuring that relationships
  between tables remain consistent.
- **Isolation Levels**: SQL databases support different isolation levels to control how transaction changes are visible
  to other users and systems, preventing issues like dirty reads, non-repeatable reads, and phantom reads.**