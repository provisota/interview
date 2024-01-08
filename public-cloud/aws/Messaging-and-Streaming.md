# Messaging and Streaming
1. **SQS (Simple Queue Service)**: SQS is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications. It eliminates the complexity and overhead associated with managing and operating message oriented middleware, and empowers developers to focus on differentiating work.

   **SNS (Simple Notification Service)**: SNS is a fully managed messaging service for both application-to-application (A2A) and application-to-person (A2P) communication. The A2A pub/sub functionality provides topics for high-throughput, push-based, many-to-many messaging between distributed systems, microservices, and event-driven serverless applications.

   **MQ (Amazon MQ)**: Amazon MQ is a managed message broker service for Apache ActiveMQ and RabbitMQ that makes it easy to set up and operate message brokers in the cloud. Message brokers allow different software systems–often using different programming languages, and on different platforms–to communicate and exchange information.

   **Pinpoint**: Amazon Pinpoint is a flexible and scalable outbound and inbound marketing communications service. It enables you to engage with your customers across multiple messaging channels.

2. **Kinesis**: Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information.

   **IoT MQTT Broker**: AWS IoT Core supports MQTT, a lightweight communication protocol specifically designed to tolerate intermittent connections, minimize the code footprint on devices, and reduce network bandwidth requirements.

   **DynamoDB Streams**: DynamoDB Streams captures a time-ordered sequence of item-level modifications in any DynamoDB table and stores this information in a log for up to 24 hours. Applications can access this log and view the data items as they appeared before and after they were modified, in near real time.

3. **Scaling**: AWS provides several services that help you scale your applications and services, such as Auto Scaling, Elastic Load Balancing, and AWS Elastic Beanstalk. You can also scale your databases using services like Amazon RDS and Amazon DynamoDB.

   **Sharding**: Sharding is a type of database partitioning that separates very large databases into smaller, faster, more easily managed parts called data shards. Amazon RDS supports sharding at the application level, and Amazon DynamoDB supports automatic sharding.

   **Integration with other services**: AWS provides several ways to integrate with other services, such as AWS Lambda for serverless compute, Amazon S3 for storage, and Amazon API Gateway for creating, deploying, and managing APIs.

   **Limitations**: Each AWS service has its own limitations. For example, Amazon SQS guarantees at-least-once message delivery, but it doesn't guarantee first in, first out delivery of messages. Amazon DynamoDB supports automatic scaling, but it might take some time for scaling to take effect. It's important to understand these limitations when designing your applications.
# Questions
1. Difference between SNS & SQS?
2. What is SQS extended client ?
3. How to consume same message from SQS by multiple consumers?
4. SQS: messages types, formats, limitations, delivery semantic, DLQ, ACKs, visibility timeout?
5. Does SQS supports ordering? what types of queues do you know?
6. Describe the difference of Aggregation and Collection for Kinesis Producer Library?
7. Kinesis usecases
8. Kinesis FanOut vs Standard consumer, sharding, limitations?
# Answers
1. **Difference between SNS & SQS**: Amazon SNS (Simple Notification Service) is a publisher/subscriber messaging system. It allows you to send messages to multiple subscribers, and these subscribers can be SQS queues, HTTP(S) endpoints, email addresses, or AWS Lambda functions. On the other hand, Amazon SQS (Simple Queue Service) is a distributed message queuing service for independently designed processing of messages. The main difference is that SNS implements a "push" mechanism, delivering messages to subscribers, while SQS implements a "pull" mechanism, where messages are pulled by consumers.

2. **SQS Extended Client**: The Amazon SQS Extended Client Library for Java enables you to manage Amazon SQS message payloads with Amazon S3. This is especially useful when you need to send a payload that exceeds the current SQS maximum message size limit (256 KB).

3. **Consume same message from SQS by multiple consumers**: In SQS, once a message is read by a consumer, it becomes invisible to other consumers based on the visibility timeout setting. If you want the same message to be processed by multiple consumers, you could use SNS to fan out messages to multiple SQS queues, each processed by a different consumer.

4. **SQS**: Messages in SQS can contain up to 256 KB of text in any format. SQS guarantees at-least-once delivery, but does not guarantee first-in, first-out delivery of messages. A dead-letter queue (DLQ) can be set up to receive messages that have failed processing. Acknowledgements (ACKs) are not explicitly sent by consumers in SQS. Instead, consumers delete the message from the queue to signal successful processing. The visibility timeout is the period of time during which Amazon SQS prevents other consumers from receiving and processing the message.

5. **SQS Supports Ordering**: Yes, SQS supports ordering in its FIFO (First-In-First-Out) queues. FIFO queues maintain the order of messages. Standard queues offer maximum throughput, best-effort ordering, and at-least-once delivery.

6. **Aggregation and Collection for Kinesis Producer Library**: Aggregation in Kinesis Producer Library (KPL) refers to the process of combining multiple records into a single Kinesis record. Collection in KPL refers to the process of grouping records together based on the partition key. Both aggregation and collection help to increase throughput and reduce costs by minimizing the number of Kinesis records.

7. **Kinesis Use Cases**: Amazon Kinesis is used for real-time processing of streaming data at massive scale. Use cases include real-time analytics, log and event data collection, real-time dashboard updates, and more.

8. **Kinesis FanOut vs Standard Consumer, Sharding, Limitations**: In Kinesis, a standard consumer uses a classic model where multiple consumers can read data from a stream in parallel. Fan-out consumers, on the other hand, use enhanced fan-out, which provides dedicated throughput per consumer while maintaining low latencies. Sharding in Kinesis is a way to increase the total capacity of a stream. Each shard provides a capacity of 1MB/sec data input and 2MB/sec data output. Some limitations of Kinesis include a retention period of up to 7 days for data records, and a maximum total capacity of a stream equal to the sum of the capacities of its shards.