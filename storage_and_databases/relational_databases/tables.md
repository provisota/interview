# Relational Database Tables

Tables are the fundamental building blocks of relational databases. They organize data into rows and columns, forming
the basis for storing and retrieving data in a structured format.

- **Rows (Records)**: Each row in a table represents a single, implicitly structured data item or record. Every row
  usually has a unique identifier known as a primary key.
- **Columns (Fields)**: Each column represents a specific attribute or field of the data item. Columns have a defined
  data type, such as integer, string, date, etc.
- **Relationships**: Tables can be related to one another through keys. A primary key in one table is used to reference
  corresponding entries in other tables (foreign keys), establishing relationships between tables.
- **[Schema](schema.md)**: Defines the structure of the table, including the columns and data types.
- **[Normalization](normalization.md)**: The process of structuring a relational database to reduce data redundancy and improve data
  integrity.

## Q&A

### How do primary keys and foreign keys work together to define relationships in relational database tables?

Primary keys and foreign keys are essential in defining relationships between tables in a relational database. A
primary key is a unique identifier for each record in a table, ensuring that each record can be uniquely identified. A
foreign key, on the other hand, is a column (or a set of columns) in one table that refers to the primary key in another
table. This connection establishes a relationship between the two tables, enabling the database to enforce referential
integrity. For example, in a database with 'Customers' and 'Orders' tables, the 'Orders' table might have a foreign key
that references the primary key of the 'Customers' table, indicating which customer placed each order. This relationship
allows for complex queries that join data from multiple tables based on these relationships.