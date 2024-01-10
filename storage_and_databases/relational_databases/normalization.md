# Relational Database Normalization

## Overview of Normalization in Relational Databases

Normalization in relational databases is the process of organizing data to minimize redundancy and improve data
integrity. It involves structuring a database in a way that reduces data dependency and anomaly.

- **[Normal Forms](../data-schema-management.md#normal-forms)**: Normalization is typically done in stages, called
  normal forms(1NF, 2NF, 3NF, BCNF, etc.). Each normal form addresses a specific type of anomaly and builds upon the
  previous form.
    - **1NF (First Normal Form)**: Ensures each column has atomic values and each row is unique.
    - **2NF (Second Normal Form)**: Achieved when it's in 1NF and all non-key attributes are fully functionally
      dependent on the primary key.
    - **3NF (Third Normal Form)**: Achieved when it's in 2NF and all the attributes are functionally independent of any
      other non-primary key attribute.
    - **BCNF (Boyce-Codd Normal Form)**: A stronger version of 3NF, addressing situations where multiple candidate keys
      are present.

- **Benefits**: Reduces data redundancy, improves data integrity, and simplifies the database structure, making it
  easier to maintain.

## Q&A

### How does normalization impact database performance and maintenance?

**Normalization, primarily, improves database maintenance and data integrity. By reducing redundancy and dependency, it
ensures that each piece of data is stored only once, reducing the amount of data duplication and storage space required.
This structure simplifies the update processes and helps in maintaining consistency, as there are fewer duplicate data
to manage.

However, highly normalized databases can sometimes lead to performance issues, especially in complex queries involving
multiple joins across normalized tables. This is because each join operation can add to the query processing time.
Therefore, in practice, a balance is often struck between normalization for data integrity and denormalization for
performance optimization, based on the specific requirements and usage patterns of the database.**