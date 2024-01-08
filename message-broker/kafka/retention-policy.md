# Retention Policy

Apache Kafka's retention policy is a crucial aspect of its data management, controlling how long data is stored on Kafka
brokers. Here are the technical details regarding Kafka's retention policy:

## Basic Concept

- **Purpose**: The retention policy in Kafka determines how long messages are kept in topics before they are deleted or
  compacted.
- **Configurable**: Retention policies are configurable at the broker level and can be overridden at the topic level.

## Types

1. **Time-Based Retention**:
    - **Default Behavior**: Messages are retained for a specified time period.
    - **Configuration**: Set using the `retention.ms` property.
    - **Common Use-Case**: Useful for scenarios where data relevance diminishes with time, such as log aggregation.

2. **Size-Based Retention**:
    - **Size Limit**: Messages are retained up to a maximum size limit of the log.
    - **Configuration**: Set using the `retention.bytes` property.
    - **Usage**: Ideal for systems with limited storage capacity.

3. **Log Compaction**:
    - **Key-Based Retention**: In log compacted topics, Kafka retains only the latest message for each key within the
      partition.
    - **Purpose**: Ensures that at least the latest data for every key is retained, beneficial for stateful
      applications.
    - **Configuration**: Enabled by setting `cleanup.policy` to `compact`.

## Configuration and Management

- **Broker-Level Configuration**: Global defaults can be set for all topics on a Kafka broker.
- **Topic-Level Configuration**: Individual topics can have their own retention settings, overriding the broker
  defaults.
- **Dynamic Configuration Changes**: Kafka allows changing retention settings without restarting brokers or clients.

## Retention Policy Internals

- **Cleanup Threads**: Kafka uses background threads to delete or compact old records based on the configured retention
  policy.
- **Segment Files**: Data in Kafka is stored in segment files. Retention operations are performed on these segments.
- **Performance Considerations**: Retention operations can consume I/O resources. Adequate monitoring and tuning are
  necessary for high-throughput environments.

## Impact on Producers and Consumers

- **Producers**: Retention policies are generally transparent to producers, which continue to append records to topics.
- **Consumers**: Consumers can only consume records that are still retained. If a consumer falls behind past the
  retention period, it may miss some records.

## Monitoring and Maintenance

- **Retention Monitoring**: It’s important to monitor disk space and segment sizes to manage retention effectively.
- **Impact on Recovery and Replication**: Retention settings can impact recovery times and replication behavior,
  particularly in failover scenarios.