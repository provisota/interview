# Messaging & Streaming
Google Cloud Pub/Sub is a messaging service that allows you to send and receive messages between independent applications. It provides a simple, reliable, scalable foundation for stream analytics and event-driven computing systems.

## Subscriber Types
There are two types of subscribers in Pub/Sub: pull and push. Pull subscribers send requests to the Pub/Sub server to retrieve messages. Push subscribers receive messages as HTTP requests from the Pub/Sub server.

## Message
A message is the data that is sent from the publisher to the subscribers. It contains two parts: the data itself, which is a blob of arbitrary data, and attributes, which is a map of key-value pairs.

## Flow
The flow of messages in Pub/Sub starts with a publisher application that sends messages to a topic. Subscriber applications then receive those messages from a subscription to that topic.

## Security
Security in Pub/Sub is handled through Identity and Access Management (IAM). You can control who can publish messages to a topic and who can subscribe to receive those messages.

## Integration with Other Services
Pub/Sub can be integrated with many Google Cloud services. For example, you can trigger a Cloud Function with a Pub/Sub message, export logs from Cloud Logging to Pub/Sub, or use Pub/Sub as an event source for Cloud Run.

# Questions
1. Describe Pub/Sub use-cases?
2. Push vs Pull models?
3. How to receive same message by different Subscribers?
4. Pub/Sub internal components and data flow?
5. What delivery semantic PubSub supports?

# Answers
1. Pub/Sub use-cases: Pub/Sub can be used in a variety of use-cases such as balancing workloads in network clusters, distributing event notifications, refreshing distributed caches, logging to multiple systems, and data streaming from various processes or devices.

2. Push vs Pull models: In the push model, Pub/Sub initiates requests to the subscriber applications to deliver messages. In the pull model, the subscriber applications initiate requests to the Pub/Sub to retrieve messages.

3. Receiving the same message by different Subscribers: In Pub/Sub, you can create multiple subscriptions to a topic. Each subscriber receives all the messages published to the topic. So, to have different subscribers receive the same message, they should all be subscribed to the same topic.

4. Pub/Sub internal components and data flow: The main components of Pub/Sub are topics and subscriptions. Publishers send messages to topics. Subscribers receive messages either by Pub/Sub pushing them to the subscriber's chosen endpoint, or by the subscriber pulling them from the service. The data flow is from publishers to topics to subscriptions to subscribers.

5. Delivery semantics PubSub supports: Pub/Sub guarantees at-least-once message delivery. That means messages are delivered to subscribers at least once, but in certain situations, a message might be delivered more than once.