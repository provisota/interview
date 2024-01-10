# Relational Database ACID Properties

ACID properties are a set of principles that ensure database transactions are processed reliably. They are critical for
maintaining the integrity of data in relational databases.

- **[Atomicity](#relational-database-acid-properties-atomicity)**: Ensures that each transaction is treated as a single,
  indivisible unit. Either all operations within the transaction are completed successfully, or none are.
- **[Consistency](#relational-database-acid-properties-consistency)**: Guarantees that a transaction brings the database
  from one valid state to another, maintaining all predefined rules, such as constraints, cascades, triggers, etc.
- **[Isolation](isolation.md)**: Ensures that concurrent execution of transactions leaves the database in the same state
  as if the transactions were executed sequentially.
- **[Durability](#relational-database-acid-properties-durability)**: Once a transaction has been committed, it will
  remain so, even in the event of power loss, crashes, or errors. In other words, the changes made by the transaction
  are permanent.

## Relational Database ACID Properties: Atomicity

Atomicity is one of the core ACID properties in relational databases, ensuring that transactions within the database are
treated as a single unit of work.

- **All-or-Nothing Principle**: Atomicity guarantees that either all operations of a transaction are completed
  successfully, or none are. If any part of the transaction fails, the entire transaction is rolled back.
- **Error Handling**: In case of system failures, errors, or interruptions, atomicity ensures that partial
  transactions are not committed to the database, thus maintaining data integrity.
- **Transactional Control**: Implemented using transactional control statements such
  as `BEGIN TRANSACTION`, `COMMIT`, and `ROLLBACK`.

### Q&A

#### How does atomicity ensure data integrity in database operations?

Atomicity ensures data integrity by applying the all-or-nothing approach to transactions. When a transaction is
initiated in a database, it may involve multiple operations like inserts, updates, or deletes. Atomicity ensures that
either all these operations are successfully executed and committed, or none are. If an error occurs during the
transaction, or if the transaction is not completed as intended, atomicity dictates that all changes made since the
beginning of the transaction are undone, leaving the database in its original state before the transaction began. This
approach prevents partial updates or inconsistent states in the database, thereby maintaining data integrity.

## Relational Database ACID Properties: Consistency

Consistency in the context of ACID properties of relational databases refers to the requirement that every transaction
brings the database from one valid state to another valid state, maintaining the integrity of the database.

- **Data Integrity**: Ensures that all data follows certain rules and constraints, such as data type, range
  constraints, and referential integrity.
- **Constraint Enforcement**: The database enforces constraints like primary keys, foreign keys, unique constraints,
  and check constraints during transactions.
- **State Transition**: A transaction can change the state of the database, but only in allowed ways that leave the
  database in a valid state.

### Q&A

#### What mechanisms do relational databases use to maintain consistency during transactions?

Relational databases maintain consistency during transactions primarily through the enforcement of constraints and
rules defined in the database schema. For example, if a transaction tries to insert a record that violates a primary key
constraint (like duplicating an existing key), the database rejects the transaction. Similarly, foreign key constraints
ensure that relations between tables remain valid. Other mechanisms include check constraints to enforce specific
conditions on data, and triggers that can perform additional checks or changes to maintain consistency. Additionally,
transactions themselves are structured to ensure that the database moves from one consistent state to another, without
leaving partially completed operations that could lead to an inconsistent state.

## Relational Database ACID Properties: Durability

Durability is a fundamental ACID property in relational databases that ensures once a transaction has been committed, it
will remain so, even in the event of a system crash or power failure. This property guarantees the permanence of
database transactions.

- **Data Persistence**: After a transaction is committed, changes made by the transaction are permanently saved to
  the database storage, ensuring data is not lost.
- **Recovery Mechanisms**: Databases use various recovery mechanisms, like write-ahead logging (WAL), to restore the
  committed state after a crash.
- **Commit Protocol**: The database management system employs a commit protocol to ensure that transaction logs are
  written to durable storage before confirming the transaction's success.

### Q&A

#### How does a database ensure durability, especially in cases of unexpected failures?

Databases ensure durability primarily through the use of transaction logs and recovery mechanisms. When a transaction
is processed, its details are first written to a transaction log, which is maintained on durable storage like a hard
drive. This process ensures that even if the database crashes or there is a power failure, the transaction information
is not lost. Upon recovery, the database can use these logs to redo transactions that were committed but not fully
executed, ensuring that the database reflects all committed transactions. This logging and recovery process is central
to maintaining the durability of transactions, providing a guarantee that once a transaction is committed, its effects
are permanently recorded in the database.

## Q&A

### How do relational databases implement the isolation property, and what are its challenges?

Isolation in relational databases is typically implemented using locking mechanisms and transaction isolation levels.
Locks prevent multiple transactions from accessing the same data simultaneously, thereby avoiding conflicts. The
transaction isolation levels (Read Uncommitted, Read Committed, Repeatable Read, and Serializable) provide different
degrees of isolation, balancing between performance and consistency.

One of the challenges in implementing isolation is the trade-off between concurrency and accuracy. Higher levels of
isolation (like Serializable) provide more accuracy but can lead to performance issues due to increased locking and
reduced concurrency. On the other hand, lower levels (like Read Committed) improve performance but are more prone to
concurrency-related issues like dirty reads or non-repeatable reads. Choosing the right level of isolation is critical
and depends on the specific requirements of the database application.