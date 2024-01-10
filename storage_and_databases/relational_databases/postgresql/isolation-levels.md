# PostgreSQL Isolation Levels

PostgreSQL supports several transaction isolation levels, as defined in the SQL standard. These levels determine how
changes made by one transaction become visible to other transactions, and they play a crucial role in handling
concurrency control. Here's a detailed look at these levels and the concurrency issues they address:

1. **Read Uncommitted**:
    - PostgreSQL does not actually implement 'Read Uncommitted'; it treats it as 'Read Committed'. In other databases,
      this level allows transactions to see uncommitted changes from other transactions (dirty reads), but PostgreSQL
      avoids this issue.

2. **Read Committed**:
    - Default level in PostgreSQL.
    - Transactions see only the data committed before they started, but they might see changes made by other
      transactions if those transactions commit while the first is still running.
    - Solves: Dirty reads.
    - Doesn't solve: Non-repeatable reads (where a transaction could read the same row multiple times and see different
      data) and phantom reads (where new rows can be added to the results of a query by another transaction).

3. **Repeatable Read**:
    - Transactions see a consistent snapshot of the database as of the start of the transaction.
    - Solves: Dirty reads and non-repeatable reads.
    - Doesn't solve: Phantom reads, although PostgreSQL's implementation using
      [Serializable Snapshot Isolation](#serializable-snapshot-isolation-ssi) (SSI) makes this less of a problem.

4. **Serializable**:
    - The strictest isolation level.
    - Ensures total isolation from other transactions, making it appear as if transactions were executed serially, one
      after the other.
    - Solves: Dirty reads, non-repeatable reads, and phantom reads.
    - Implementation: PostgreSQL uses [SSI](#serializable-snapshot-isolation-ssi), which detects serialization conflicts
      between concurrent transactions at commit time and rolls back transactions as necessary.

## Multi-Version Concurrency Control (MVCC)

PostgreSQL uses Multi-Version Concurrency Control (MVCC) to implement these isolation levels. MVCC works by giving each
transaction a snapshot of the database at a specific point in time:

- **[Snapshots](#snapshots)**: When a transaction starts, it gets a snapshot of the database. This snapshot determines
  which version of each row the transaction can see.
- **[Versioning](#versioning)**: Instead of locking rows for updates, PostgreSQL creates a new version of a row each
  time it is updated. Older versions are kept for transactions that need to see them.
- **Visibility Rules**: A set of rules determines whether a transaction can see a particular version of a row based on
  transaction IDs and the age of the row versions.

### Snapshots

PostgreSQL's Multi-Version Concurrency Control (MVCC) system and its use of snapshots are central to how it manages data
consistency and handles concurrent access to the database.

#### Basic Concept of MVCC

1. **Versioning**: Instead of locking rows when they are written to, PostgreSQL creates a new version of a row each time
   it is updated or deleted. These versions are called 'tuples'. The original version is not overwritten but kept,
   allowing multiple versions of a row to exist simultaneously.

2. **Transaction ID**: Every transaction in PostgreSQL is assigned a unique transaction ID (XID). This ID is used to
   track which transactions have created or modified each row version.

#### Creating Snapshots

1. **Snapshot Creation**: When a transaction starts, PostgreSQL creates a snapshot of the database for it. This snapshot
   contains information about the transaction IDs of all active transactions (i.e., transactions that were in progress
   when the snapshot was taken) and the highest transaction ID that had been assigned when the snapshot was created.

2. **Visibility Rules**: The snapshot determines which version of each row is visible to the transaction, based on the
   transaction IDs associated with each row version and the snapshot's data. This ensures that the transaction sees a
   consistent view of the database.

#### Visibility Determination

1. **Visible Changes**: A transaction can see the changes made by other transactions that were committed before the
   snapshot was taken. It cannot see changes made by transactions that started after or were still in progress when the
   snapshot was taken.

2. **Row Versioning**: Each row version (tuple) in PostgreSQL is tagged with the transaction ID of the transaction that
   created it. Additionally, if a row is deleted or updated, information about the deleting/updating transaction is
   stored.

3. **Checking Visibility**: When a transaction looks at a row, PostgreSQL uses the transaction IDs in the row version
   and the information in the snapshot to determine if the row version is visible to the transaction. This involves
   checking whether the row version was created by a transaction that had committed before the snapshot was taken and
   not deleted by a transaction that had committed before the snapshot was taken.

#### Advantages of MVCC and Snapshots

- **Concurrency**: Multiple transactions can read and write data concurrently without locking rows. This significantly
  reduces lock contention.

- **Consistency**: Each transaction sees a consistent view of the data as of the time the snapshot was taken, regardless
  of changes made by other transactions.

- **Non-blocking Reads**: Read operations do not block write operations and vice versa, leading to higher performance in
  multi-user environments.

#### Caveats

- **Transaction ID Wraparound**: Since transaction IDs are finite, PostgreSQL must periodically perform vacuuming to
  prevent ID exhaustion, a process known as transaction ID wraparound.

- **Vacuuming**: PostgreSQL periodically runs a process called vacuuming to remove old row versions that are no longer
  visible to any transactions, helping to reclaim space and prevent bloat.

In summary, PostgreSQL's use of MVCC with snapshots allows transactions to see a consistent view of the database at the
moment they start, ensuring data consistency while allowing high levels of concurrency. This system elegantly handles
the complexities of multi-user database access.

### Versioning

Multi-Version Concurrency Control (MVCC) in PostgreSQL is a strategy for managing concurrent access to the database that
avoids the need for many types of read and write locks, thereby increasing performance, especially in multi-user
environments.

1. **Tuple Versions**: In PostgreSQL, each row of a table is referred to as a 'tuple'. Under MVCC, each time a tuple is
   updated or deleted, a new version of that tuple is created. These versions are stored in the same table and are
   sometimes referred to as 'tuple versions' or 'row versions'.

2. **Transaction IDs**: Each tuple version is associated with a transaction ID (XID). This ID indicates the transaction
   that created this version of the tuple. When a tuple is updated or deleted, the new version of the tuple (or the
   deletion marker) carries the transaction ID of the modifying transaction.

#### How Versioning Works

1. **Inserts**: When a new tuple is inserted, it is assigned the transaction ID of the inserting transaction. This tuple
   becomes visible to all transactions that start after the inserting transaction commits.

2. **Updates**: An update to a tuple in PostgreSQL is handled as a combination of an insert and a delete. The old
   version of the tuple is marked as deleted by the updating transaction, and a new version of the tuple is inserted
   with the transaction ID of the updating transaction.

3. **Deletes**: When a tuple is deleted, instead of being removed from the table, it is marked with a deletion
   transaction ID, indicating that it has been deleted by that transaction.

#### Visibility Rules

1. **Transaction Snapshots**: Each transaction in PostgreSQL works with a snapshot of the database taken at the start of
   the transaction. This snapshot includes information about the transaction IDs that were active when the snapshot was
   created.

2. **Visibility Determination**: Whether a particular version of a tuple is visible to a transaction depends on its
   transaction ID relative to the IDs in the transaction's snapshot:
    - A tuple version is visible if it was created by a transaction that committed before the snapshot was taken.
    - A tuple version is not visible if it was created by a transaction that started after the snapshot or is yet to
      commit.

#### Garbage Collection and Vacuuming

- **Old Tuple Versions**: Over time, as tuples are updated and deleted, old versions accumulate. These are not needed
  once no transaction can see them.

- **Vacuum Process**: PostgreSQL periodically runs a process called 'vacuuming'. This process cleans up old tuple
  versions that are no longer visible to any transactions, reclaiming storage space and maintaining database
  performance.

#### Benefits of MVCC Versioning

- **Concurrency**: By allowing multiple versions of tuples to coexist, MVCC increases concurrency. Transactions can
  operate on different versions of tuples without interfering with each other, reducing the need for locking and
  increasing throughput.

- **Consistency**: Transactions see a consistent state of the database, as of the time their snapshot was taken,
  regardless of concurrent modifications.

- **Non-Blocking Reads**: Read operations are generally non-blocking, as they can work with the snapshot of the data,
  irrespective of concurrent write operations.

MVCC in PostgreSQL is a sophisticated mechanism that balances the needs for consistency, concurrency, and performance in
a multi-user database environment. The versioning of tuples allows transactions to proceed without waiting for each
other, while still ensuring that each transaction sees a consistent and isolated view of the database.

Certainly! To illustrate how PostgreSQL's MVCC (Multi-Version Concurrency Control) versioning works, let's look at some
sample scenarios involving transactions and row versioning. These examples will help demonstrate how different versions
of a row are created and maintained, and how transactions interact with these versions based on their isolation level.

#### Sample Scenario: Insert, Update, and Delete Operations

##### Initial State:

- Table `users` with columns `id` and `name`.
- Existing row: `id = 1, name = 'Alice'`.

##### Transactions and Operations:

1. **Transaction A** starts.
2. **Transaction B** starts.
3. **Transaction A** inserts a new row into `users`: `id = 2, name = 'Bob'`.
4. **Transaction A** commits.
5. **Transaction C** starts.
6. **Transaction C** updates the `name` of `id = 2` to 'Robert'.
7. **Transaction C** commits.
8. **Transaction B** tries to read `id = 2`.

##### How MVCC Handles This:

- When **Transaction A** inserts the new row and commits, a new version of the row (`id = 2, name = 'Bob'`) is created
  with Transaction A's ID.
- When **Transaction C** updates the row, it creates a new version (`id = 2, name = 'Robert'`) and marks the old version
  as obsolete.
- Since **Transaction B** started before Transaction A committed, it will not see the row inserted by Transaction A.
  This is because the snapshot for Transaction B does not include changes made by transactions that committed after it
  started.

##### Behavior Under Different Isolation Levels:

###### 1. Read Uncommitted (Not truly available in PostgreSQL, behaves like Read Committed):

- **Transaction B** will see the changes immediately after they are made, even if the transactions that made these
  changes have not committed yet.
- In PostgreSQL, since it treats Read Uncommitted as Read Committed, **Transaction B** will see the new
  row (`id = 2, name = 'Bob'`) after **Transaction A** commits and `name = 'Robert'` after **Transaction C** commits.

###### 2. Read Committed (Default in PostgreSQL):

- **Transaction B** will see changes only after they are committed.
- **Transaction B** will not see the row with `id = 2` when **Transaction A** is still in progress. It
  sees `id = 2, name = 'Bob'` only after **Transaction A** commits.
- After **Transaction C** commits, if **Transaction B** queries again, it will see `id = 2, name = 'Robert'`.

###### 3. Repeatable Read:

- **Transaction B** will see the database as it was when **Transaction B** started, regardless of commits made by other
  transactions after **Transaction B** started.
- **Transaction B** will not see the row `id = 2` at all, as it was inserted after **Transaction B** started.
- Changes made by **Transaction C** will also not be visible to **Transaction B**, even if it queries again.

###### 4. Serializable:

- This is the strictest level, similar to Repeatable Read in terms of visibility. Additionally, it ensures a sequence of
  transactions is serializable.
- **Transaction B** behaves like in Repeatable Read, not seeing any changes made after it started.
- Serializable adds checks to prevent concurrent transactions from conflicting in a way that could not be achieved if
  the transactions were run serially, one after another. If such a conflict is detected, one of the transactions will be
  rolled back with a serialization failure.

##### Summary:

- **Read Uncommitted**: Transactions see ongoing changes (PostgreSQL treats as Read Committed).
- **Read Committed**: Transactions see changes only after they are committed.
- **Repeatable Read**: Transactions see a consistent snapshot of the database as it was when they started.
- **Serializable**: Similar to Repeatable Read in terms of data visibility, with additional checks to prevent
  non-serializable execution patterns.

#### Sample Scenario: Concurrency and Visibility

##### Initial State:

- Table `orders` with columns `order_id`, `product`, and `quantity`.
- Existing rows: `order_id = 1, product = 'Book', quantity = 10`.

##### Transactions and Operations:

1. **Transaction X** starts.
2. **Transaction Y** starts.
3. **Transaction X** updates `quantity` to 15 for `order_id = 1`.
4. **Transaction Y** reads the quantity for `order_id = 1`.
5. **Transaction X** commits.
6. **Transaction Y** reads the quantity for `order_id = 1` again.

##### How MVCC Handles This:

- **Transaction X** creates a new version of the row with the updated quantity, but this new version is only visible to
  Transaction X until it commits.
- When **Transaction Y** first reads the quantity, it sees the original quantity (10) because Transaction X has not
  committed yet.
- After **Transaction X** commits, if **Transaction Y** reads the quantity again, whether it sees the new quantity (15)
  depends on its isolation level. Under "Read Committed," it sees the new quantity; under "Repeatable Read," it
  continues to see the original quantity.

##### Sample Scenario: Vacuuming and Old Versions

##### Scenario Description:

- Over time, many updates and deletes happen on a table `products`.
- Old versions of rows accumulate.

##### Vacuuming Process:

- PostgreSQL runs a vacuum process periodically.
- This process removes old versions of rows that are no longer visible to any transactions.
- It helps in reclaiming space and maintaining database performance.

These examples demonstrate how PostgreSQL’s MVCC handles different versions of data and maintains consistency across
various transactions, depending on their start times and isolation levels. Vacuuming is an essential maintenance
activity to manage the accumulation of old row versions.

In PostgreSQL, the visibility of data in a table is governed by its Multi-Version Concurrency Control (MVCC) system.
MVCC ensures that each transaction sees a consistent view of the data without being affected by other concurrently
running transactions. Here's a detailed look at the visibility rules under PostgreSQL's MVCC:

### Visibility Rules

Core Concepts:

1. **Transaction ID (XID)**: Every transaction is assigned a unique transaction ID.
2. **Tuple Versioning**: Each row (or tuple) in a table may have multiple versions, each created by different
   transactions. These versions are tagged with the XID of the transaction that created or modified them.
3. **Snapshots**: A snapshot is created at the start of each transaction. It includes the XID of the transaction, a list
   of active transaction IDs at that time, and the highest transaction ID assigned when the snapshot was taken.

The visibility of a row version (tuple) to a transaction is determined based on several factors:

1. **Transaction IDs**:
    - A row version is visible to a transaction if it was created by a committed transaction that completed before the
      transaction's snapshot was taken.
    - A row version created by the transaction itself is always visible to that transaction.

2. **Insert Visibility**:
    - A newly inserted row version is visible to the transaction that inserted it and to any other transactions that
      start after the inserting transaction commits.

3. **Update Visibility**:
    - When a row is updated, a new version is created. This new version is visible to the updating transaction and to
      transactions that start after the update is committed.
    - The previous version remains visible to transactions for whom it was visible, based on their snapshots.

4. **Delete Visibility**:
    - When a row is deleted, it is not physically removed but marked as deleted by the transaction ID of the deleting
      transaction.
    - This row version becomes invisible to transactions that start after the delete operation commits.

5. **Concurrency and Isolation Levels**:
    - The visibility of row versions can vary based on the transaction's isolation level. For instance, at the "
      Serializable" level, a transaction will see a consistent view of the database as of the moment it started,
      regardless of changes made by other transactions.

#### Vacuuming and Old Row Versions

- **Vacuum Process**: PostgreSQL periodically runs a vacuum process to clean up old row versions that are no longer
  visible to any transaction. This is necessary to reclaim space and prevent the database from growing indefinitely.
- **Freezing**: To manage the finite size of transaction IDs, old row versions may be "frozen". A frozen row version is
  made permanently visible to all transactions, effectively ignoring its original transaction ID.

#### Summary

In PostgreSQL's MVCC:

- Each transaction sees a consistent view of the database as of the time its snapshot was taken.
- The visibility of row versions depends on the transaction IDs and the snapshot of each transaction.
- Special processes like vacuuming and freezing are used to manage old row versions and maintain the efficiency and
  integrity of the database.

This MVCC approach allows PostgreSQL to handle high levels of concurrency while ensuring data integrity and consistency
across transactions.

## Serializable Snapshot Isolation (SSI)

Serializable Snapshot Isolation (SSI) in PostgreSQL is an advanced mechanism for handling transactions at the highest
level of isolation, ensuring serializability. This level of isolation prevents phenomena like dirty reads,
non-repeatable reads, and phantom reads, which can occur at lower isolation levels. It guarantees that even though
transactions may execute concurrently, the outcome is as if they were executed one after the other in some order.

### Key Concepts of Serializable Snapshot Isolation

1. **Consistent Snapshot**: Each transaction in Serializable isolation mode gets a snapshot of the database at the
   moment it begins. This snapshot represents a consistent view of the database state, and the transaction interacts
   with this state throughout its duration.

2. **Detecting Conflicts**: The primary challenge in maintaining serializability is detecting and resolving conflicts
   between concurrent transactions. PostgreSQL's SSI mechanism does this by tracking data dependencies between
   transactions.

3. **Read/Write Dependencies**: When a transaction reads data, it creates a read dependency on the transaction that last
   wrote that data. Similarly, write operations create write dependencies. These dependencies are tracked to detect
   potential serialization conflicts.

### How SSI Works

1. **Transaction Execution**: Transactions proceed normally, operating on their consistent snapshot of the database.

2. **Dependency Tracking**: PostgreSQL tracks the interactions between transactions, noting when one transaction's
   operations depend on the data read or written by another.

3. **Conflict Detection**: At commit time, the system checks for serialization conflicts, which occur when the
   dependencies between transactions would not be possible in any serial (one after the other) ordering of those
   transactions.

4. **Conflict Resolution**: When a conflict is detected, PostgreSQL resolves it by aborting and rolling back one of the
   conflicting transactions. The aborted transaction can then be retried.

### Advantages of Serializable Snapshot Isolation

- **High Concurrency**: SSI allows for a high degree of concurrency while still providing strong consistency guarantees.

- **No Locking**: Unlike traditional serializable isolation which often relies on locking mechanisms, SSI achieves
  serializability primarily through versioning and dependency tracking, reducing lock contention.

- **Performance**: For many workloads, especially those with more read operations than write operations, SSI can offer
  better performance than traditional serializable isolation.

### Use Cases for SSI in PostgreSQL

- **Financial Transactions**: Ensuring the integrity of financial transactions, where it's critical to maintain strict
  consistency.

- **High-Integrity Systems**: Applications where data consistency is paramount, and any data anomalies caused by
  concurrent access are unacceptable.

- **Complex Transactions**: Scenarios involving complex operations or calculations where intermediate states should not
  be visible or interfered with by other transactions.

SSI in PostgreSQL represents a sophisticated approach to transaction management, balancing the need for strong data
consistency with the demands for high concurrency. It's particularly useful in scenarios where data integrity is
critical, and the cost of occasional transaction rollbacks is acceptable compared to the benefit of maintaining a strict
consistency model.

## Concurrency Issues Addressed

1. **Dirty Reads**: Occur when a transaction reads data written by a concurrent uncommitted transaction. PostgreSQL's
   Read Committed and higher levels prevent this.

2. **Non-repeatable Reads**: Happen when a transaction reads the same row twice and gets different data because another
   transaction modified the row between the two reads. Prevented by Repeatable Read and higher levels.

3. **Phantom Reads**: Occur when a transaction re-executes a query returning a set of rows that satisfy a search
   condition and finds that the set of rows satisfying the condition has changed due to another recently-committed
   transaction. Serializable isolation level prevents this in PostgreSQL.

In summary, PostgreSQL's implementation of transaction isolation levels, primarily through MVCC and SSI for the
Serializable level, effectively addresses various concurrency issues, ensuring data integrity and consistency in a
multi-user environment.