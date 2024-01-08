# Indexes

Indexes in databases are critical for improving the speed of data retrieval operations. They function similarly to
indexes in books, allowing the database to find data without scanning every row in a table. Here's an overview of
technical details on indexes and potential interview questions:

### Technical Details on Indexes

1. **Purpose**: Primarily used to speed up the retrieval of data from a database table.

2. **Types of Indexes**:
    - **Single-Column Indexes**: An index created on a single column of a table.
    - **Composite Indexes**: An index on two or more columns of a table.
    - **Unique Indexes**: Ensures that the index key contains only unique values.
    - **Full-Text Indexes**: Designed for text-based columns to improve the performance of full-text queries.

3. **How Indexes Work**:
    - They maintain a smaller, separate data structure (such as B-trees, hash tables) that stores key fields for quick
      searching.
    - When a query is executed, the database uses the index to locate the data quickly without scanning the entire
      table.

4. **Performance Considerations**:
    - While indexes significantly improve query speed, they also require additional storage space.
    - Indexes can slow down write operations (INSERT, UPDATE, DELETE) because the index needs to be updated whenever the
      data is altered.

5. **Choosing Columns for Indexing**:
    - Columns frequently used in the WHERE clause, JOIN operations, or as part of an ORDER BY clause are good candidates
      for indexing.

## Q&A
### How Do You Decide Which Columns to Index in a Database Table?

**Answer**:

- Index columns that are frequently used in query predicates (WHERE clause) or join conditions.
- Consider the selectivity of the column (columns with high uniqueness are better candidates).
- Avoid over-indexing columns that are not often used in queries, as this can impact write performance.

### What is the Difference Between a Clustered and a Non-Clustered Index?

**Answer**:

- **Clustered Index**: Defines the order in which data is physically stored in the table. There can be only one
  clustered index per table, which is why it's usually on the primary key.
- **Non-Clustered Index**: Stores data in one place and indices in another. A table can have multiple non-clustered
  indexes.

### Can You Explain the Impact of Indexes on Database Performance?

**Answer**:

- Indexes greatly improve read query performance by allowing the database to locate data faster.
- However, they can negatively impact write performance since the indexes must be updated each time the data is
  modified.
- The key is to find a balance between optimizing read performance and minimizing the overhead on write operations.

### What are Full-Text Indexes and When Would You Use Them?

**Answer**:

- Full-text indexes are specialized indexes used for text searching, often in large textual columns. They enable
  efficient querying of text data, like searching for specific words or phrases within strings.
- They are used in scenarios where the requirement is to perform complex searches against large text fields, such as
  searching articles, descriptions, or reviews.

### How Can Over-Indexing Affect Database Performance?

**Answer**:

- Over-indexing can lead to unnecessary consumption of disk space and can degrade write performance. Each additional
  index requires maintenance and updating whenever a data modification operation occurs, which can slow down INSERT,
  UPDATE, and DELETE operations.