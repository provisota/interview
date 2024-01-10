# Relational Database Primary Key

A primary key is a field (or a combination of fields) in a relational database table that uniquely identifies each
record within the table. It is a fundamental aspect of database design and plays a crucial role in maintaining data
integrity and optimizing database performance.

- **Unique Identification**: Each primary key value must be unique within its table. No two rows can have the same
  primary key value.
- **Non-null**: A primary key cannot contain NULL values. Each record must have a value for the primary key.
- **Indexing**: The database automatically creates an index for the primary key, which speeds up data retrieval.
- **Referential Integrity**: Primary keys are used to define relationships with other tables (through foreign keys) and
  ensure referential integrity.

## Q&A

### How does a primary key enhance data integrity and efficiency in a relational database?

A primary key enhances data integrity by ensuring that each record in a table can be uniquely identified, preventing
duplicate entries. This unique identification is crucial for establishing clear relationships between tables through
foreign keys, maintaining the referential integrity of the database. From an efficiency perspective, the primary key is
automatically indexed, which significantly improves the speed of queries that search or sort by the primary key field.
This indexing allows the database management system to quickly locate and retrieve records, leading to faster and more
efficient database operations.