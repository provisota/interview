# Relational Database Schema

A relational database schema is a blueprint of how a database is structured. It defines the tables, fields (columns),
relationships, and constraints within the database.

- **Tables**: The schema specifies the tables in the database and what data each table will hold.
- **Fields (Columns)**: Each table is made up of fields, and the schema defines the type of data each field holds (e.g.,
  integer, text, date).
- **Primary Keys**: Defined for each table to uniquely identify each row (record).
- **Foreign Keys**: Establish relationships between tables, linking each record in one table to a record in another.
- **Constraints**: Rules set on data in the database, such as `NOT NULL`, `UNIQUE`, `CHECK`, and `DEFAULT` constraints,
  to ensure data integrity.
- **Indexes**: Created to improve the speed of data retrieval.

## Q&A

### How does the schema design impact the performance and integrity of a relational database?

**Schema design is crucial for both performance and data integrity in a relational database. Good schema design, with
properly defined keys, indexes, and normalization, ensures efficient data storage, quick retrieval, and minimal
redundancy. Properly defined primary and foreign keys enforce data integrity, ensuring accurate relationships between
tables. Constraints like `NOT NULL` and `UNIQUE` prevent incorrect or duplicate data entry. Moreover, well-designed
indexes significantly improve query performance by reducing the time it takes to locate specific rows within tables.
Poor schema design, on the other hand, can lead to redundant and inconsistent data, inefficient queries, and ultimately,
a system that is difficult to maintain and scale.**