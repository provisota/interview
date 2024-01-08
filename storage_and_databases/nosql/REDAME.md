# Scope
1. NoSQL DB Types and Use Cases:
    - Document Databases (e.g., MongoDB, CouchDB): These are used when data is semi-structured and can be grouped together. They store data in a document-like format (usually JSON).
    - Key-Value Stores (e.g., Redis, DynamoDB): These are simple and fast, used for caching, session management, and serving real-time data.
    - Wide-Column Stores (e.g., Cassandra, HBase): These are used when large amounts of data need to be stored and retrieved quickly. They are great for analyzing large datasets.
    - Graph Databases (e.g., Neo4j, Amazon Neptune): These are used when dealing with interconnected data. They are great for social networks, recommendation engines, etc.

2. CAP/PACELC Implications on Distributed Databases:
    - CAP Theorem (Consistency, Availability, Partition Tolerance): It states that in the event of a network partition, a distributed system can either remain completely consistent or available, but not both. Different NoSQL databases prioritize different aspects. For example, Cassandra prioritizes Availability and Partition Tolerance (AP) while HBase prioritizes Consistency and Partition Tolerance (CP).
    - PACELC Theorem (Partition, Availability, Consistency, Else, Latency, Consistency): It extends the CAP theorem by stating that even in the absence of a network partition, a trade-off exists between latency and consistency. For example, a database might choose to write data to multiple nodes before considering the write successful (strong consistency) which increases latency, or it might consider the write successful after writing to a single node (eventual consistency) which decreases latency.
# Questions
1. Which types of non-relational databses do you know?
2. Describe usecases for each type you mentioned earlier.
3. What are BASE transactions? What is the difference in comparison with ACID? (Note: This is pure theoretical question. Alternatively ask about eventual consistency, e.g. what it means, ask for some examples).
4. Describe the implication of the CAP (or PACELC) theorem on the database of your choice
5. Describe the internal architecture of database of your choice.
6. Describe how the databse of your choice handle writes.
# Answers
1. There are four main types of NoSQL databases:
    - Document Databases (e.g., MongoDB, CouchDB)
    - Key-Value Stores (e.g., Redis, DynamoDB)
    - Wide-Column Stores (e.g., Cassandra, HBase)
    - Graph Databases (e.g., Neo4j, Amazon Neptune)

2. Use cases for each type:
    - Document Databases: These are used when data is semi-structured and can be grouped together. They store data in a document-like format (usually JSON), making them ideal for content management systems, catalogues, and user profiles.
    - Key-Value Stores: These are simple and fast, used for caching, session management, and serving real-time data. They are ideal for shopping carts, user preferences, and real-time bidding.
    - Wide-Column Stores: These are used when large amounts of data need to be stored and retrieved quickly. They are great for analyzing large datasets, making them ideal for Internet of Things (IoT) data, time-series data, and event logging.
    - Graph Databases: These are used when dealing with interconnected data. They are great for social networks, recommendation engines, and fraud detection.

3. BASE transactions are a different approach to database transactions than ACID. BASE stands for Basically Available, Soft state, Eventually consistent. Unlike ACID transactions, which aim for consistency at the end of each transaction, BASE transactions allow for a period of inconsistency following a transaction, but promise eventual consistency. This makes BASE transactions more suitable for distributed systems where immediate consistency can be difficult to achieve.

4. Let's consider Cassandra, a wide-column store, for the CAP theorem implications. Cassandra prioritizes Availability and Partition Tolerance (AP). This means that in the event of a network partition, Cassandra will continue to function, but it may not provide the most recent write. Once the partition is resolved, it will become consistent again. This is suitable for use cases where availability is prioritized over immediate consistency.

5. Cassandra's internal architecture is based on a ring design instead of a master-slave design. All nodes in Cassandra are the same; there is no concept of a master node, with all nodes communicating with each other via a gossip protocol. Data is distributed among all nodes and can be accessed quickly via any node. This design provides high availability and no single point of failure.

6. In Cassandra, writes are handled by first writing data to a commit log for durability, and then writing the data to an in-memory structure called a memtable. Once the memtable is full, it is flushed to disk as an SSTable. All writes are automatically partitioned and replicated throughout the cluster. Cassandra also provides tunable consistency - for each read or write operation, you can specify how many replicas must respond before the operation is considered successful.