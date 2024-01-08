# Scope
Message Queue and Streaming Queue are both methods of inter-process communication in distributed systems, but they have different use cases and characteristics.

1. Message Queue:
    - Message Queues like RabbitMQ, ActiveMQ, and ZeroMQ are typically used for asynchronous communication between services. They allow one service to send a message to another without waiting for a response.
    - Message Queues provide a way to decouple services and can handle high volumes of messages. They ensure that messages are delivered at least once and in the order they were sent.
    - RabbitMQ and ActiveMQ support various messaging models like point-to-point, publish-subscribe, and request-reply. They also provide features like message durability, acknowledgments, and prefetching.
    - ZeroMQ is a lightweight messaging library that provides various messaging patterns like request-reply, publish-subscribe, and push-pull.

2. Streaming Queue:
    - Streaming Queues like Kafka are used for real-time data processing. They allow services to publish and subscribe to streams of records.
    - Kafka is designed to handle real-time data feeds with low latency. It retains all messages for a set amount of time, and consumers can read messages from any point in the stream.
    - Kafka provides features like message durability, fault-tolerance, and real-time processing. It also supports both batch and real-time use cases.

3. Duplicates Handling, Ordering, Error Handling:
    - Both Message Queues and Streaming Queues provide mechanisms to handle duplicates, maintain message order, and handle errors.
    - In RabbitMQ and ActiveMQ, duplicates can be avoided by ensuring that each message has a unique ID. Kafka handles duplicates by using a message key.
    - For message ordering, RabbitMQ and ActiveMQ guarantee order within a single queue. Kafka maintains order within a partition.
    - Error handling is typically done through acknowledgments and retries. Both RabbitMQ and Kafka support automatic retries and negative acknowledgments.
# Questions
1. What is stream?
2. What is Pub/Sub pattern?
3. Pub/sub model vs Events stream model?
4. What is structured and unstructured streams? How to deal with each one?
5. What is message queue?
6. Message queue vs Streaming queue?
7. RabbitMQ exchange strategies?
8. Downsides of streaming queue in microservices?
9. How to handle message ordering in both queue types?
10. What is dead letter pattern? When to use and how to process?
11. How to process duplicates? How they can happen?
12. What is consumer groups in Kafka? How they work?
13. What is topic in kafka? What is partition in Kafka?
14. How process stream data on consumer side? Example: time windows, aggregations
15. RabbitMQ's architecture?
16. Kafka architecture
17. RabbitMQ vs ActiveMQ?
18. How to organize streams? stream per service? one stream for all services? stream per event type?
19. How to calculate amount of partitions in Kafka for proper setup?
20. Compare
# Answers
1. A stream is a sequence of data elements made available over time. It is particularly useful when working with large datasets, or real-time data feeds, as it allows you to process data on the fly without having to load the entire dataset into memory.

2. The Pub/Sub (Publish/Subscribe) pattern is a messaging pattern where senders (publishers) send messages to a channel without knowing who the recipients (subscribers) are. Subscribers express interest in one or more channels, and only receive messages that are of interest, without knowing who the publishers are.

3. The main difference between the Pub/Sub model and Event Streaming model is that in Pub/Sub, once a message is delivered, it is gone. In Event Streaming, messages are retained, forming a continuous and replayable log of events that can be consumed in real time or retrospectively.

4. Structured streams are those where the data is organized and can be processed and accessed in a structured manner. Unstructured streams are those where the data does not have a pre-defined data model or is not organized in a pre-defined manner. To deal with each one, you would typically use different processing methods. For structured streams, you can use SQL-like queries or DataFrame/Dataset APIs. For unstructured streams, you might need to use lower-level APIs like RDDs.

5. A message queue is a form of asynchronous service-to-service communication. It is used in serverless and microservices architectures. Messages are stored on the queue until they are processed and deleted.

6. The main difference between a message queue and a streaming queue is that a message queue is designed to hold messages until they are consumed or until a certain period of time has passed. A streaming queue, on the other hand, is designed to hold and distribute a stream of messages to one or more consumers.

7. RabbitMQ supports several exchange types: Direct, Topic, Headers and Fanout. Direct exchange delivers messages to queues based on a message routing key. Topic exchange routes messages to queues based on wildcard matches between the routing key and the routing pattern. Headers exchange routes messages based on header values instead of routing keys. Fanout exchange routes messages to all the queues it knows.

8. One downside of using streaming queues in microservices is the complexity of managing and monitoring multiple streams. Another downside is the potential for increased latency due to the time it takes to process and transmit streams of messages.

9. Message ordering in both queue types can be handled by assigning sequence numbers to messages or by using timestamps. However, maintaining order in distributed systems can be challenging and may require additional mechanisms such as ordering guarantees provided by the queue service.

10. The Dead Letter pattern is a way of handling failed messages. When a message cannot be processed, it is moved to a separate queue (the dead-letter queue) where it can be inspected and the issue causing the failure can be addressed.

11. Duplicates can occur due to network issues, application crashes, or other reasons. They can be handled by implementing idempotency on the consumer side (ensuring that processing a message more than once does not change the outcome), or by using a deduplication mechanism on the producer side.

12. Consumer groups in Kafka are a way of allowing a pool of consumers to divide up the work of processing records from one or more topics. Each consumer in the group will read from a unique subset of partitions of the topics the group is subscribed to.

13. A topic in Kafka is a category or feed name to which records are published. Topics in Kafka are always multi-subscriber. A partition is a single log. Topics are split into partitions for better distribution and parallelism.

14. To process stream data on the consumer side, you can use Kafka's Streams API. This allows you to perform operations like map, filter, and aggregate on the stream of records. For example, you can use the `groupByKey` and `windowedBy` methods to perform windowed aggregation on the stream.

15. RabbitMQ's architecture is based on the AMQP protocol. It includes producers, exchanges, queues, bindings, and consumers. Producers send messages to exchanges, which route them to queues based on bindings. Consumers then receive messages from queues.

16. Kafka's architecture includes producers, topics, brokers, partitions, consumers, and consumer groups. Producers send records to topics. Each topic is split into partitions and replicated across brokers for fault tolerance. Consumers read from topics and are grouped into consumer groups for load balancing.

17. RabbitMQ and ActiveMQ are both message brokers, but they have some differences. RabbitMQ is known for its robustness, ease of use, and support for a variety of messaging protocols. ActiveMQ, on the other hand, is known for its powerful JMS and JavaEE capabilities.

18. How to organize streams depends on the specific requirements of your application. You might choose to have a stream per service if each service requires different types of data. Having one stream for all services can simplify the architecture, but it might lead to unnecessary data being sent to services. Having a stream per event type can make it easier to handle different types of events.

19. The number of partitions in Kafka can be calculated based on factors like the throughput requirements, the number of consumers, and the maximum message size. More partitions allow greater parallelism for consumption, but this will also result in more total resources being used by the Kafka cluster.

20. Comparing different technologies or patterns would require more specific criteria. Could you please provide more details about what aspects you are interested in comparing?