<!-- TOC -->
* [Log Structure](#log-structure)
  * [Basic Concept](#basic-concept)
  * [Partition Log Structure](#partition-log-structure)
    * [Segments](#segments)
    * [Log Segments](#log-segments)
    * [Structure of a Segment](#structure-of-a-segment)
    * [Segment Size and Management](#segment-size-and-management)
    * [Benefits of Segment-Based Logs](#benefits-of-segment-based-logs)
    * [Compaction and Deletion](#compaction-and-deletion)
    * [Handling Failures and Corruption](#handling-failures-and-corruption)
    * [Configuration Considerations](#configuration-considerations)
  * [Offset Management](#offset-management)
    * [Offsets](#offsets)
    * [Basic Concept](#basic-concept-1)
    * [Offset Management in Kafka](#offset-management-in-kafka)
    * [Consumer Offset Tracking](#consumer-offset-tracking)
    * [Offset Reset Behavior](#offset-reset-behavior)
    * [Use in Consumer Groups](#use-in-consumer-groups)
    * [Guarantees and Delivery Semantics](#guarantees-and-delivery-semantics)
    * [Implications for Data Processing](#implications-for-data-processing)
  * [File Storage](#file-storage)
  * [Segment Size and Retention](#segment-size-and-retention)
  * [Compaction](#compaction)
  * [Replication](#replication)
  * [Performance Implications](#performance-implications)
  * [Durability](#durability)
<!-- TOC -->

# Log Structure

Apache Kafka's log structure is a core aspect of its design, enabling its high throughput, scalability, and
fault-tolerance capabilities.

## Basic Concept

- **Log**: In Kafka, a log is an ordered set of records (messages), differing from the traditional idea of logging
  messages.
- **Partition**: Each Kafka topic is split into one or more partitions, with each partition essentially being a log.

## Partition Log Structure

- **Segments**: A partition's log is divided into segments, each being a physical file on the disk.
- **Immutable Records**: Records within a segment are immutable, enabling efficient writes and reads due to their
  append-only nature.

### Segments

Apache Kafka's partition log structure is a key aspect of its performance and scalability. The log for each partition is
divided into segments, which are fundamental to how Kafka stores and manages data.

### Log Segments

- **Segment Files**: A partition's log is divided into multiple segment files. Each segment file contains a subset of
  records in the partition.
- **Immutability of Segments**: Each segment file, once written and closed, becomes immutable. This ensures efficient
  and sequential disk I/O operations.

### Structure of a Segment

1. **Data Log File**: Contains the actual records. Its name typically includes the base offset of the records in the
   file (e.g., `0000000000000123456.log`).
2. **Index Files**: Accompany data log files for faster lookups.
    - **Offset Index File**: Maps offsets to physical positions in the data log file.
    - **Time Index File**: Maps timestamps to offsets, enabling time-based searches.

### Segment Size and Management

- **Configurable Size**: The size of each segment is configurable. Once a segment file reaches its maximum size, Kafka
  closes it and starts a new segment.
- **Retention and Cleanup**: Old segments are deleted or compacted based on the topic's retention policy.

### Benefits of Segment-Based Logs

- **Performance**: Sequential writes to and reads from segment files are efficient on disk.
- **Scalability**: Segmentation allows Kafka to handle very large volumes of data by breaking logs into manageable
  chunks.
- **Retention Efficiency**: Kafka can clean up old data efficiently by deleting entire segment files.

### Compaction and Deletion

- **Deletion**: In a deletion-based retention policy, Kafka simply deletes old segments that are beyond the retention
  period.
- **Log Compaction**: In this mode, Kafka retains only the latest message for each key within the partition. Compaction
  occurs at the segment level, with older segments being compacted first.

### Handling Failures and Corruption

- **Corruption Recovery**: If a segment file is corrupted, Kafka can recover data up to the point of corruption.
- **Replication**: Each segment of a partition log is replicated across multiple brokers for fault tolerance.

### Configuration Considerations

- **Segment Size**: Larger segments can improve throughput but may increase latency and affect log compaction and
  retention.
- **Retention Policy**: The configuration of log retention impacts how long segments are kept before being deleted or
  compacted.

The segment-based log structure is central to Kafka's architecture, providing a scalable and efficient way to store and
process the continuous stream of records that Kafka handles. This structure allows Kafka to offer high performance and
durability, which are essential for modern data streaming applications.

## Offset Management

- **Offsets**: Records in a log are identified by sequential IDs called offsets, unique within each partition.
- **Commit Log**: Kafka operates as a commit log, appending every record sent to a partition at the end of the log.

### Offsets

Apache Kafka's offset management is a crucial component of its messaging capabilities, ensuring message order within
each partition and enabling consumers to track their progress.

### Basic Concept

- **Offset**: In Kafka, an offset is a unique identifier for each record within a partition. It denotes the position of
  a record in the partition.
- **Ordered Sequence**: Offsets are assigned in an ordered, increasing sequence as new records are appended to the
  partition.

### Offset Management in Kafka

1. **Assignment by Broker**: Offsets are assigned by the Kafka broker when a record is appended to a partition.
2. **Immutable**: Once assigned, an offset does not change. It remains constant for the life of the record in the log.
3. **Per-Partition**: Offsets are specific to a partition; thus, each partition has its own sequence of offsets starting
   from zero.

### Consumer Offset Tracking

- **Consumer Commit**: Consumers track their progress by committing offsets. When a consumer commits an offset, it
  indicates to Kafka that it has successfully processed all prior records.
- **Commit Storage**: The committed offsets are stored in a special Kafka topic named `__consumer_offsets`.
- **Automatic vs Manual Commit**: Consumers can be configured to commit offsets automatically at regular intervals or to
  manually commit offsets after processing messages.

### Offset Reset Behavior

- **[Consumer Group Rebalance](./consumer-group-rebalance.md)**: If a consumer group loses members or gains new ones, it
  may need to reset its offsets. Kafka provides several strategies for this, such as `earliest`, `latest`, or `none`.
- **Offset Out of Range**: If a consumer requests an offset that no longer exists (e.g., due to log retention policies),
  Kafka allows the consumer to choose how to reset the offset.

### Use in Consumer Groups

- **Parallel Consumption**: Within a consumer group, each consumer reads from exclusive partitions, and offsets help
  ensure that each consumer knows which records it has processed.
- **Fault Tolerance**: If a consumer fails, another consumer in the group can pick up processing from the last committed
  offset.

### Guarantees and Delivery Semantics

- **At-Least-Once Delivery**: If consumers commit offsets after processing messages, Kafka provides at-least-once
  delivery semantics.
- **Exactly-Once Processing**: Kafka can also support exactly-once processing semantics through the use of transactions
  and careful offset and state management.

### Implications for Data Processing

- **Order Guarantee**: Within a single partition, Kafka guarantees order based on offsets, which is crucial for many
  streaming applications.
- **Replayability**: Since offsets are stable and ordered, Kafka supports replaying data from a specific point in the
  log.

Offset management in Kafka is a powerful mechanism that enables consumers to maintain their state regarding message
consumption. It is fundamental to achieving reliable, ordered message processing in distributed systems and forms the
basis for Kafka's delivery guarantees and consumer group coordination.

## File Storage

- **File Naming**: Segment files are named to reflect their offsets, aiding in quick identification.
- **Index Files**: Kafka maintains index files for each log segment, mapping offsets to file positions for rapid record
  location.

## Segment Size and Retention

- **Configuration**: The maximum size of log segment files is configurable. Once this size is reached, a new segment is
  created.
- **Retention Policy**: Retention policies, based on time or size, govern the deletion of old segments.

## Compaction

- **Log Compaction**: Kafka features log compaction for topics, keeping only the latest value for each key and removing
  older duplicates.

## Replication

- **Leader and Followers**: Each partition has a leader and follower replicas, with the leader handling all read and
  write requests.
- **Consistency**: Followers replicate the leader's log for consistency, and a follower can become a new leader in case
  of leader failure.

## Performance Implications

- **Write Efficiency**: The append-only log allows for faster sequential disk writes.
- **Read Efficiency**: Sequential disk reads are efficient, complemented by indexes for quick message access.

## Durability

- **Sync and Flush**: Producers can choose the level of durability for their records, either immediate disk writes or
  temporary memory caching.

Kafka's log structure is key to its ability to provide high throughput and reliable data storage and retrieval. This
structure, along with Kafka's distributed nature, makes it highly effective for large-scale, real-time data streaming
and processing.