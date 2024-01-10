# Kafka

Apache Kafka is a distributed streaming platform that has gained widespread popularity due to its high throughput,
reliability, and scalability.

## Core Components

- **Producer**: Responsible for publishing records to Kafka topics.
- **Consumer**: Consumes records from Kafka topics.
- **Broker**: A Kafka server that stores data and serves clients (producers and consumers).
- **Topic**: A category or feed name to which records are published. Topics in Kafka are multi-subscriber and can have
  zero or more consumers that subscribe to the data.
- **Partition**: Topics are split into partitions, which are the fundamental parallelism and scalability unit in Kafka.

## Data Storage and Distribution

- **[Log Structure](./log-structure.md)**: Each partition is an ordered, immutable sequence of records known as a
  log. Each record in a partition is assigned a unique offset.
- **[Replication](./replication.md)**: Kafka replicates partitions across multiple brokers for fault tolerance. One
  broker serves as the leader for a given partition, handling all reads and writes, while others are followers that
  replicate the leader.
- **[Retention Policy](./retention-policy.md)**: Kafka stores records for a configurable period, after which old records
  are discarded. Data can be retained based on time or size.

## Producer Details

- **Partitioning**: Producers can specify a partition key to determine which partition a record should be sent to. If no
  key is specified, Kafka defaults to a round-robin approach.
- **Acknowledgments (ACKs)**: Producers can configure the acknowledgment level to ensure data reliability during
  transmission.

## Consumer Details

- **Consumer Groups**: Consumers are labeled with a consumer group name, and each record published to a topic is
  delivered to one consumer instance within each subscribing consumer group.
- **Offsets**: Kafka maintains a record of the last offset read by a consumer group in each partition. Consumers can
  commit offsets, and in case of a failure, Kafka will provide records from the last committed offset.

## Reliability and Durability

- **Fault Tolerance**: Kafka's replication ensures that data is not lost if a broker fails.
- **[Exactly-once Semantics](semantics/exactly-once_semantics.md) (EOS)**: Kafka supports exactly-once processing
  semantics to prevent data
  duplication.

## Semantics

- **[At Least Once](semantics/at-least-once_semantics.md)**: Kafka guarantees that a message will be delivered at least
  once to a consumer.
- **[At Most Once](semantics/at-most-once_semantics.md)**: Kafka guarantees that a message will be delivered at most
  once to a consumer.
- **[Exactly Once](semantics/exactly-once_semantics.md)**: Kafka guarantees that a message will be delivered exactly
  once to a consumer.

[Comparison](semantics/README.md#semantics-comparison)

## Scalability

- **Horizontal Scaling**: Kafka clusters can be expanded without downtime. New brokers can be added, and Kafka will
  [rebalance](./cluster-rebalancing.md) partitions across the cluster.

## Performance Optimization

- **[Batch Processing](./batch-processing.md)**: Producers and consumers can operate in batch mode, improving
  throughput.
- **[Compression](compression.md)**: Kafka supports message compression.

## Security

- **Authentication**: Kafka supports authentication via SSL or SASL.
- **Authorization**: Access control can be managed using
  [Access Control Lists](../../security/authentication-and-authorization.md#access-control-lists-acls) (ACLs).
- **Encryption**: Supports SSL/TLS for encrypting data in transit.

## Stream Processing

- **[Kafka Streams](kafka-streams.md)**: A client library for building applications and microservices where input and
  output data are stored in Kafka clusters.

## Connectors and Integration

- **[Kafka Connect](kafka-connect.md)**: A tool for scalable and reliably streaming data between Apache Kafka and other
  systems.

## Ecosystem and Tooling

- **[Schema Registry](schema-registry.md)**: For managing and evolving schemas effectively.
- **KSQL**: A SQL-like language for streaming processing on top of Kafka.

Apache Kafka is designed to handle high volumes of data and support real-time data processing, making it a key component
in the technology stack of many organizations for event-driven architectures, logging, tracking, and more.

## Topic

- A **topic** is a category or feed name to which records are published. Topics in Kafka are split into one or more
  partitions.
- Topics are the way producers (which publish messages) and consumers (which read messages) are decoupled. Producers
  write data to topics and consumers read from topics.

## Partition

- Each topic can have one or more **partitions**, allowing the data to be scaled. Partitioning allows Kafka to
  parallelize processing as each partition can be placed on a different server.
- Partitions are ordered, immutable sequences of records that are continually appended to—a structured commit log.
- Records in partitions are each assigned a unique offset. Kafka maintains this order within each partition.

## Partition Key

- When a producer sends a message to a topic, it can specify a **partition key**.
- The partition key is used by Kafka to decide which partition to place the record in. Records with the same key are
  sent to the same partition, ensuring order within that key.
- If no partition key is specified, Kafka distributes messages to partitions in a round-robin manner, providing load
  balancing over the partitions.

## Consumer Group

- A **consumer group** includes the set of consumer processes that are subscribing to a topic.
- Each consumer in a group reads from exclusive partitions of the topic. If there are more consumers than partitions,
  some consumers will be idle. If there are more partitions than consumers in a group, a consumer will read from
  multiple partitions.
- Consumer groups enable Kafka to provide both messaging semantics: broadcasting (sending a message to all consumers)
  and publishing/subscribing (sending a message to any one of the group of consumers).

## The Relationship

1. **Producer to Topic**: A producer sends messages to a Kafka topic. If a partition key is provided, Kafka uses it to
   determine the partition within the topic where the message will be placed. If no key is provided, Kafka will
   distribute messages across partitions in a balanced way.

2. **Topic to Consumer Group**: Each consumer group independently consumes messages from the topic. Kafka ensures that
   each partition is only consumed by one consumer in the group at a time, which provides load balancing and fault
   tolerance.

3. **Partitions and Consumer Scalability**: The number of partitions in a topic affects scalability and throughput. More
   partitions allow more consumers to read from a topic concurrently, up to the number of partitions.

Certainly! Let's consider a real-world scenario for an e-commerce platform and how Kafka's concepts of topic, partition
key, and consumer group play a role:

## Scenario: E-commerce Platform

### Topic: "OrderEvents"

- **Use Case**: This topic is used to publish various order-related events such as order creation, payment processing,
  and order completion.
- **Real-World Example**: When a customer places an order on the platform, an "Order Created" event is published to
  the "OrderEvents" topic.

### Partition Key: "Customer ID"

- **Use Case**: The partition key ensures that all events related to a specific customer's order are in the same
  partition, preserving the order of events.
- **Real-World Example**: Suppose customer with ID `C123` places multiple orders. Using `C123` as the partition key
  ensures that all events related to this customer's orders are sent to the same partition. This is crucial for
  maintaining the sequence of events (like order placed, payment processed, etc.) for that customer.

### Consumer Group: "InventoryService" and "NotificationService"

- **Use Groups**: Different services consume the same messages for different purposes.
- **Real-World Examples**:
    - **InventoryService**: This consumer group is responsible for updating inventory based on order events. When it
      receives an "Order Created" event, it decreases the stock for the ordered items.
    - **NotificationService**: Another consumer group that sends notifications to customers. It listens to the same "
      OrderEvents" topic. When it receives an "Order Created" event, it sends an order confirmation email to the
      customer.

### How They Interact

1. **Order Creation**: When an order is placed, an "Order Created" event with the customer ID as the partition key is
   published to the "OrderEvents" topic.
2. **Event Distribution**: Kafka ensures that all events for a specific customer (partition key) go to the same
   partition. This maintains the order of events for each customer.
3. **Concurrent Processing**:
    - The "InventoryService" consumer group reads the event, updates the inventory, and processes the order.
    - Simultaneously, the "NotificationService" group reads the same event and sends a confirmation email to the
      customer.

## Q&A

### What is Apache Kafka and what are its key features?

**Answer**: Apache Kafka is a distributed streaming platform primarily used for building real-time data pipelines and
streaming applications. It is capable of handling high-throughput data streams. Key features include:

- **High Throughput**: Kafka can handle thousands of messages per second.
- **Scalability**: Easily scalable both horizontally and vertically.
- **Fault Tolerance**: Replicates data and supports multi-node clusters for fault tolerance.
- **Durability**: Stores streams of records (messages) in topics which are durable and reliable.
- **Real-Time Processing**: Enables real-time data processing capabilities.

### Explain how Kafka's Producer-Consumer model works.

**Answer**: In Kafka, the producer is the entity that publishes records to topics, which are the categories or feeds to
which records are published. Consumers then subscribe to these topics to retrieve and process these records. Kafka
maintains a queue of records in the form of topics which are divided into partitions to allow multiple consumers to read
in parallel, leading to high throughput.

### Describe Kafka’s storage mechanism.

**Answer**: Kafka stores records in topics, which are split into partitions. Each partition is an ordered, immutable
sequence of records that is continually appended to. These records are stored as a set of log files on the disk. Kafka
retains all messages for a set amount of time, and each message within a partition is assigned a sequential ID number
called an offset.

### What is a Kafka Topic and Partition?

**Answer**: A Kafka topic is a category or feed name to which records are published. Topics in Kafka are divided into
partitions to allow for data parallelism. Partitions allow multiple consumers to read from a topic concurrently. Each
partition is an ordered, immutable sequence of records.

### How does Kafka ensure fault tolerance?

**Answer**: Kafka ensures fault tolerance through replication. Each partition of a topic can be replicated across
multiple nodes in a Kafka cluster. In case of a node failure, one of the replicas can serve as the new leader for the
partition to ensure continuous availability of data.

### Can you explain the concept of a Consumer Group in Kafka?

**Answer**: A Consumer Group in Kafka is a group of consumers which jointly consume data from a topic. Each consumer
within a group reads from exclusive partitions of the topic. This model allows Kafka to provide both broadcasting (
sending a message to all consumers) and publish-subscribe (sending a message to any one consumer in the group) messaging
models.

### What are some common challenges or problems you might encounter while working with Kafka?

**Answer**: Common challenges with Kafka include:

- **Data Loss**: Although rare, it can occur, particularly in improperly configured systems.
- **Performance Bottlenecks**: This can happen if there are too many messages, not enough partitions, or insufficient
  consumer processing power.
- **Schema Management**: Ensuring compatibility of message formats over time can be challenging.
- **Monitoring and Operations**: Kafka requires careful monitoring and operational procedures to run smoothly and
  efficiently.

### How do you handle schema evolution in Kafka?

**Answer**: Schema evolution in Kafka is typically handled using a schema registry, like the Confluent Schema Registry.
It allows producers and consumers to register schemas and provides compatibility checks to ensure that the schema
changes do not break consumers.

### What is Kafka Streams?

**Answer**: Kafka Streams is a client library for building applications and microservices where the input and output
data are stored in Kafka clusters. It provides a simple and lightweight API to process data stored in Kafka. It supports
exactly-once processing semantics and allows for stateful and stateless processing.

### How would you secure a Kafka cluster?

**Answer**: Securing a Kafka cluster involves:

- **Authentication**: Using SSL or SASL to authenticate clients.
- **Authorization**: Implementing ACLs (Access Control Lists) to control access to topics.
- **Encryption**: Encrypting data in transit using SSL.
- **Monitoring and Auditing**: Implementing tools for monitoring and auditing access and usage.

Preparing comprehensive answers to these questions will showcase your understanding of Kafka and its ecosystem during a
technical interview.