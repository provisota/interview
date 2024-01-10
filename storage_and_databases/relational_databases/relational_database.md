# Relational Database

A relational database is a type of database that stores and provides access to data points that are related to one
another. It's based on the relational model proposed by E.F. Codd.

- **[Tables](tables.md)**: Data is organized in tables, which consist of rows and columns. Each row is
  a record, and each column is a field.
- **[Schema](schema.md)**: Defines the structure of the database, including tables, fields, and the
  data types for each field.
- **[Primary Key](primary-key.md)**: A unique identifier for each record in a table.
- **[Foreign Key](foreign-key.md)**: A field in one table that links to a primary key in another
  table, establishing a relationship between the two tables.
- **[SQL](sql.md) (Structured Query Language)**: A standard language used to query and manipulate
  relational databases.
- **[Normalization](normalization.md)**: The process of organizing data to minimize redundancy and dependency.
- **[ACID Properties](ACID.md)**: Relational databases typically ensure Atomicity, Consistency, Isolation, and
  Durability, crucial for reliable data transactions.

## Q&A

### What are the advantages of using a relational database?

Relational databases offer several advantages:

- **Structured Organization**: They provide a clear and structured schema for data, making it easy to organize and
  retrieve.
- **Data Integrity**: The use of primary and foreign keys ensures relationships between tables and data integrity.
- **Scalability and Flexibility**: While they are best suited for structured data, relational databases can be scaled to
  handle large amounts of data and complex queries.
- **ACID Compliance**: Ensures reliable transactions, which is critical for data accuracy and consistency.
- **Mature Technology**: Relational databases have been around for decades, offering robustness, reliability, and a vast
  ecosystem of tools and support.