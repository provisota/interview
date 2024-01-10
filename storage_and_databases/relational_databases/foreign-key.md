# Relational Database Foreign Key

A foreign key in a relational database is a field (or collection of fields) in one table that uniquely identifies a row
of another table. The foreign key is defined in a table (child table) and refers to the primary key in another table (
parent table). It is a fundamental concept used to maintain referential integrity between two data tables.

- **Referential Integrity**: Ensures relationships between tables are consistent. For instance, if Table B has a foreign
  key that references Table A, every value of the foreign key in Table B must exist as a primary key in Table A.
- **Relationships**: Foreign keys define the relationships between tables, such as one-to-one, one-to-many, and
  many-to-many.
- **Cascading Actions**: Actions such as `CASCADE DELETE` or `CASCADE UPDATE` ensure changes in the parent table are
  automatically reflected in the child table.

## Q&A

### How does a foreign key relationship affect data manipulation in a relational database?

A foreign key relationship affects data manipulation by ensuring data integrity between the related tables. When a
foreign key constraint is in place, any attempt to add a record to the child table with a foreign key value that doesn't
exist in the parent table's primary key will be rejected. This prevents orphan records in the child table. Similarly,
attempts to delete or change a record in the parent table that is referenced by a foreign key in the child table can be
controlled. For instance, the database can be set to prevent such deletion (referential integrity) or to cascade the
delete to the child table (cascade delete). Thus, foreign key relationships enforce consistent data maintenance rules
across tables and prevent the creation of invalid references.