# Scope
1. Enterprise Integration Patterns: These are design patterns that provide a standardized methodology to integrate different systems in a loosely coupled manner. They include patterns like Message Channel, Message Router, Message Translator, and Message Endpoint.

2. Saga: This is a design pattern that provides a way to define a series of local transactions that can be executed in a distributed environment. Each local transaction updates data within a single service and publishes an event to trigger the next local transaction in the saga.

3. Shared DB: This is a pattern where multiple services share the same database. While this can simplify data management, it can also lead to tight coupling between services and make it harder to evolve the schema.

4. Transactional Outbox: This is a pattern that can be used to maintain data consistency across services in a microservices architecture. Each service publishes events to an outbox database table during local transactions. A separate process then retrieves the events and publishes them to a message channel.

5. Transactional Log: This is a pattern where changes to a database are recorded in a log that can be used to replicate the changes to other databases or to replay transactions for recovery purposes.

6. Sidecar: This is a pattern where each service in a microservices architecture is paired with a secondary service (the sidecar) that provides supporting features like monitoring, logging, configuration, etc. The sidecar runs in the same process or container as the main service and can enhance or extend its functionality.
# Questions
1. provide several examples of integration patterns
2. what is Transactional Log and what tools usually uses it
3. what Transactional outbox pattern gives to application
4. Give an example of Sidecar pattern usage. how it is related to singe node pattern?
5. what is saga? what it is for?
6. What is shared DB, cons/pros of such approach
7. Compare orchestration vs choreography in saga implementation
# Answers
1. Examples of integration patterns include:
    - API Gateway: A server that acts as an API front-end, receives API requests, enforces throttling and security policies, passes requests to the back-end service and then passes the response back to the requester.
    - Message Broker: An architectural pattern for message validation, transformation, and routing. It mediates communication among applications, minimizing the mutual awareness that applications should have of each other in order to be able to exchange messages.
    - Event-Driven Architecture: A software architecture pattern promoting the production, detection, consumption of, and reaction to events.

2. A Transactional Log (also known as a transaction log, database log, binary log or audit trail) is a history of actions executed by a database management system to guarantee ACID properties over crashes or hardware failures. Physically, a log is a file of updates done to the database, stored in stable storage. Tools that use transactional logs include relational databases like MySQL, PostgreSQL, and SQL Server.

3. The Transactional Outbox pattern is a method used in microservices architecture to maintain data consistency across services. Each service publishes events to an outbox database table during local transactions. A separate process then retrieves the events and publishes them to a message channel. This ensures that the event is published exactly once, and in the correct order.

4. The Sidecar pattern is a technique where each service in a microservices architecture is paired with a secondary service (the sidecar) that provides supporting features like monitoring, logging, configuration, etc. The sidecar runs in the same process or container as the main service and can enhance or extend its functionality. For example, a sidecar container could be used to handle logging for a main application container. It's related to the single-node pattern in that both the main application and the sidecar run on the same node.

5. A Saga is a design pattern that provides a way to define a series of local transactions that can be executed in a distributed environment. Each local transaction updates data within a single service and publishes an event to trigger the next local transaction in the saga. It's used to ensure data consistency across multiple services in a microservices architecture.

6. A Shared Database is a pattern where multiple services share the same database. While this can simplify data management, it can also lead to tight coupling between services and make it harder to evolve the schema. Pros of this approach include simplicity and strong consistency. Cons include tight coupling, reduced flexibility, and potential for performance bottlenecks.

7. In a Saga, orchestration vs choreography refers to how the individual local transactions are coordinated:
    - Orchestration: There is a central coordinator (an orchestrator) that tells the participants what local transaction to execute. The orchestrator is responsible for central decision-making and sequencing the steps of the transaction.
    - Choreography: Each local transaction publishes domain events that trigger the next local transaction. There is no central coordinator. Instead, each participant knows which event it needs to react to and what local transaction it needs to execute.