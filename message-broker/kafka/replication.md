<!-- TOC -->
* [Replication](#replication)
  * [Basic Concept](#basic-concept)
  * [Leader and Follower Model](#leader-and-follower-model)
  * [Replication Process](#replication-process)
  * [Consistency and Durability](#consistency-and-durability)
  * [Handling Failures](#handling-failures)
  * [Configuration Parameters](#configuration-parameters)
  * [Performance Considerations](#performance-considerations)
  * [Monitoring and Maintenance](#monitoring-and-maintenance)
<!-- TOC -->

# Replication

Apache Kafka's replication mechanism is a fundamental feature that ensures high availability and durability of data.

## Basic Concept

- **Purpose**: Replication in Kafka is designed to provide fault tolerance and high availability by copying data across
  multiple nodes (brokers) in a Kafka cluster.
- **Replica**: Each partition in Kafka has one or more replicas, meaning that the same data is stored on multiple
  brokers.

## Leader and Follower Model

- **Leader Replica**: For each partition, one of the replicas is designated as the leader. All produce and consume
  requests for that partition are served by the leader.
- **Follower Replicas**: The other replicas are followers. They passively replicate the leader’s log and do not serve
  client requests directly.

## Replication Process

1. **Data Writing**: Producers write data to the leader of the partition.
2. **Data Replication**: The leader appends the data to its log and then replicates it to its followers.
3. **Acknowledgment**: Depending on the configuration, the leader either waits for acknowledgments from followers before
   considering a write successful or proceeds without waiting.

## Consistency and Durability

- **In-Sync Replicas (ISR)**: Kafka maintains a list of replicas that are in-sync, meaning they are caught up to the
  leader.
- **Durability Guarantees**: A message is considered committed when all in-sync replicas have appended the message to
  their log. This ensures data is not lost if a broker fails.

## Handling Failures

- **Leader Election**: If a leader replica fails, one of the in-sync follower replicas is elected as the new leader.
- **Replica Lag**: Kafka constantly monitors the lag of each replica. If a follower falls too far behind, it can be
  removed from the ISR list.

## Configuration Parameters

- **Replication Factor**: This setting determines the number of replicas for each partition.
- **Min ISR**: The minimum number of replicas that must acknowledge a write for it to be considered successful.
- **Ack Mode**: Producers can choose their acknowledgment mode - `acks=0` (no acknowledgment), `acks=1` (only leader
  acknowledgment), or `acks=all` (acknowledgment from all in-sync replicas).

## Performance Considerations

- **Throughput vs Durability**: Higher replication factors can provide better durability but may impact throughput and
  latency due to the overhead of replicating data across more brokers.
- **Network Bandwidth**: Replication consumes network bandwidth, which is an important factor in cluster design.

## Monitoring and Maintenance

- **Monitoring Replication**: It’s crucial to monitor replication lag and the health of replicas to ensure data
  integrity.
- **[Cluster Rebalancing](./cluster-rebalancing.md)**: When adding or removing brokers, Kafka can rebalance partitions
  and replicas across the cluster.