# At least once semantics

Apache Kafka's at-least-once semantics is a delivery guarantee that ensures messages are delivered at least once to the
consumer, meaning messages are not lost but may be duplicated. This semantic is often the default choice for many
Kafka-based applications due to its balance between performance and reliability.

## Basic Concept

- **Primary Goal**: To prevent message loss. Each message is guaranteed to be delivered at least once, but it may be
  delivered more than once.
- **Duplication Possibility**: Because of retries and network issues, the same message might be delivered and processed
  multiple times.

## Implementing At-Least-Once Semantics in Kafka

1. **Producer Configuration**:
    - **Acknowledgements (ACKs)**: Producers are typically configured to wait for acknowledgments from the broker.
      Setting `acks` to `1` or `all` ensures that messages are not considered successfully sent until acknowledged by
      the broker.
    - **Retries**: The producer may retry sending messages if acknowledgments are not received within a specified
      timeout, which can lead to duplicate messages.

2. **Consumer Processing**:
    - **Offset Committing**: Consumers commit offsets after processing messages. If a consumer commits the offset and
      then crashes before processing the message completely, the same message might be read and processed again after
      the consumer restarts.
    - **Idempotent Processing**: To handle potential duplicates, the consumer's processing logic often needs to be
      idempotent (i.e., processing the same message multiple times does not impact the overall system state).

## Broker Configuration and Handling

- **Replication and Durability**: Kafka brokers are configured with replication to ensure messages are not lost.
  Messages are stored persistently on disk and replicated across multiple brokers.

## Challenges and Considerations

- **Performance vs. Reliability**: At-least-once semantics strike a balance between performance and reliability. While
  it prevents data loss, it can lead to duplicated processing, which might be acceptable for many applications.
- **Application Logic**: The consuming application must be designed to handle duplicate messages, either by processing
  them idempotently or by implementing logic to detect and ignore duplicates.

## Use Cases

- **Logging and Monitoring**: Systems where duplicate messages are not critical and can be handled or ignored.
- **Event Processing**: In many event-driven architectures, the system is designed to handle or tolerate duplicate
  events.

## Trade-offs

- **Throughput and Latency**: At-least-once semantics might have a higher throughput and lower latency compared to
  exactly-once semantics, as it does not incur the overhead of ensuring exactly-once delivery.
- **Complexity**: The consumer application might need additional logic to handle duplicates, which can add complexity to
  the application design.

Kafka's at-least-once semantics is widely used due to its balance between ensuring data is not lost and maintaining
reasonable throughput and latency. However, it requires applications to be aware of and capable of handling message
duplicates, either through idempotent processing or duplicate detection.