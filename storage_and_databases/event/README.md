# Scope
1. Message Delivery Guarantees, Deduplication:
    - Message delivery guarantees are assurances that messages sent from a producer to a consumer will be delivered without failure. There are typically three types of delivery guarantees: At most once, At least once, and Exactly once.
    - Deduplication is the process of ensuring that only unique messages are processed in situations where the same message might be delivered more than once. This is particularly important in systems that guarantee at least once delivery, as they may deliver the same message multiple times in an effort to ensure that it is processed.

2. Difference between Message Processing Systems (RabbitMQ vs Kafka), Processing Patterns, Message Ordering, Performance and Throughput Optimizations:
    - RabbitMQ is a traditional message broker with a variety of messaging patterns and point-to-point queuing. It's designed for reliable delivery of messages, supporting various messaging protocols and has a variety of features like message queuing, delivery acknowledgment, and flexible routing to queues.

    - Kafka, on the other hand, is a distributed streaming platform designed for high volume real-time data feeds. It's more of a distributed commit log service than a traditional message broker. Kafka retains all messages for a set amount of time, and consumers are responsible for tracking their location in each log (offset). Therefore, Kafka can support a large number of consumers and retain large amounts of data with very little overhead.

    - In terms of processing patterns, RabbitMQ is more versatile and supports multiple messaging protocols and can handle high-throughput scenarios. Kafka is designed for high throughput and distributed environments, and it excels in real-time processing and streaming data use cases.

    - For message ordering, Kafka maintains the order of messages within a partition. This means that if message A is sent before message B, Kafka guarantees that message A will be read before message B. However, if messages are sent to different partitions, the order can't be guaranteed. RabbitMQ, on the other hand, guarantees message order within a single queue only.

    - Performance and throughput optimizations often involve fine-tuning configurations like batch size, buffer memory, and compression for Kafka, and prefetch count and acknowledgement modes for RabbitMQ. Both systems can be scaled horizontally for increased performance and throughput.
# Questions
1. What message delivery guarantees do you know?
2. Why consumer should be idempotent?
3. What differences between PUSH(Rabbit) and PULL (Kafka)?
4. What is pub/sub and when it to be used?
5. How would you implement request reply pattern?
6. What options are provided to guarantee message ordering?
7. How to optimize kafka producer?
8. How to optimize kafka consumers?
9. How would you choose number of partitions?
# Answers
1. There are typically three types of message delivery guarantees:
    - At most once: Messages are delivered once and never redelivered. This can result in lost messages if a failure occurs.
    - At least once: Messages are guaranteed to be delivered, but they may be delivered more than once. This requires the consumer to be idempotent.
    - Exactly once: Messages are guaranteed to be delivered once and only once. This is the hardest to achieve and often requires cooperation between the producer, broker, and consumer.

2. A consumer should be idempotent to handle the scenario of "at least once" delivery guarantee. If a message is delivered more than once, the consumer should be able to process it without causing duplicate side effects.

3. The main difference between PUSH (RabbitMQ) and PULL (Kafka) is in the way messages are delivered to consumers. In a PUSH model, the broker pushes the message to the consumer as soon as it arrives. In a PULL model, the consumer requests the message from the broker when it's ready to process the message.

4. Pub/Sub (Publish/Subscribe) is a messaging pattern where producers (publishers) do not program the messages to be sent directly to specific receivers (subscribers). Instead, published messages are characterized into classes, without knowledge of what (if any) subscribers there may be. It's commonly used in one-to-many communication, is time decoupled, and can be used to notify changes to multiple consumers.

5. The request-reply pattern can be implemented using two queues. The client sends a message with a correlation ID on the request queue and then listens on the reply queue for a message with the same correlation ID.

6. Message ordering can be guaranteed in a few ways. In Kafka, messages sent by a producer to a particular topic partition will be appended in the order they are sent. Consumers can consume the messages in the order they were stored in the log.

7. Kafka producer can be optimized by batching messages together, compressing message batches, and tuning the `linger.ms` and `batch.size` configurations.

8. Kafka consumers can be optimized by increasing the number of consumer threads, increasing the fetch size, and tuning the `max.poll.records` configuration.

9. The number of partitions in Kafka is chosen based on the throughput requirements. More partitions allow greater parallelism for consumption, but this will also result in more total resources being used by the Kafka cluster. You should choose a number that can handle your producer throughput, but also keep in mind that more partitions may increase end-to-end latency and affect the availability of your Kafka cluster.