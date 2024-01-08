# Messaging

## Queue Storage
Azure Queue Storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.

## Service Bus
Azure Service Bus is a fully managed enterprise integration message broker. It can decouple applications and services from each other, providing secure, reliable message delivery.

## Questions
1. Compare Queue Storage and Service Bus. What are the advantages of each of them?
2. Describe the flow of Topics and Subscriptions in Service Bus.
3. What kind of filters can be applied on a Topic (boolean, sql, correlation)?
4. Describe the concepts of Message Sessions, Autoforwarding, Dead-letter Queue.
5. What security protocols are supported by service bus?

## Answers
1. Queue Storage is best for large-volume workloads, and it provides cost-effective message storage. Service Bus is best for enterprise-level messaging and supports advanced features like FIFO, batching/sessions, transactions, dead-lettering, temporal control, routing and filtering, and duplicate detection.
2. In Service Bus, a message is sent to a Topic, and then delivered to one or more associated Subscriptions, depending on filter rules that can be set on a per-subscription basis.
3. Service Bus Topics support SQL-like expression filters, Correlation filters, and the TrueFilter and FalseFilter.
4. Message Sessions enable joint and ordered handling of unbounded sequences of related messages. Autoforwarding enables automatic forwarding of a message from a queue or subscription to another queue or topic. Dead-lettering sends a message to the dead-letter queue if it can't be processed or if it's expired.
5. Service Bus supports Shared Access Signature (SAS) authentication, Role-Based Access Control (RBAC) with Azure Active Directory, and Managed identities for Azure resources.