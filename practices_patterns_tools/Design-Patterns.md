# Design patterns
GoF (Gang of Four) refers to the four authors of the book "Design Patterns: Elements of Reusable Object-Oriented Software". This book describes 23 design patterns that can be useful in software development. The patterns are categorized into three groups: Creational, Structural, and Behavioral.

DDD (Domain-Driven Design) is an approach to software development that emphasizes the importance of understanding the business domain, creating a domain model, and using a ubiquitous language that is shared by both developers and business stakeholders. It aims to align software development with business needs.

CQRS (Command Query Responsibility Segregation) is a pattern that separates read and write operations for a data store. It can improve performance, scalability, and security, but it can also increase complexity because it requires synchronization between the read and write models.

Event Sourcing is a pattern where state changes are logged as a sequence of events. This allows you to reconstruct the state of an object at any point in time, and it also provides a full audit trail of changes. However, it can be complex to implement and it requires careful consideration of how to handle events that may be out of order or in error.
# Questions
1. What are the benefit (usage) of design patterns for software engineers?
2. Enumerate design patterns groups/types according to GoF classification.
3. What is DDD, why is it useful?
4. What is bounded context in DDD?
5. Enumerate and describe DDD building blocks.
6. What is CQRS?
7. What is Event Sourcing?
8. What are CQRS usecases and pros/cons?
9. Name Event Sourcing usecases and pros/cons.
10. How to handle external queries (queries to external systems/apis) in event sourcing?
# Answers
1. Design patterns provide a standard terminology and are specific to particular scenario. They offer solutions to common design problems in object-oriented software development. The benefits of using design patterns for software engineers include:
    - Reusability: Design patterns provide solutions that can be reused in multiple projects.
    - Best Practices: Design patterns represent best practices and can help to avoid potential problems in the code.
    - Communication: Design patterns provide a standard terminology that can improve communication between developers.

2. According to the Gang of Four (GoF) classification, design patterns are divided into three groups:
    - Creational Patterns: Deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. Examples include Singleton, Factory, and Builder.
    - Structural Patterns: Deal with object composition, ensuring that different parts of a system work together properly. Examples include Adapter, Decorator, and Proxy.
    - Behavioral Patterns: Deal with communication between objects, how they interact and distribute responsibilities. Examples include Observer, Strategy, and Command.

3. Domain-Driven Design (DDD) is an approach to software development that emphasizes the importance of understanding the business domain, creating a domain model, and using a ubiquitous language that is shared by both developers and business stakeholders. It's useful because it aligns software development with business needs, leading to software that is more likely to meet the business's requirements and easier to maintain and evolve.

4. In DDD, a Bounded Context is a logical boundary within which a particular model is defined and applicable. It encapsulates a specific functionality and contains models, services, and a specific ubiquitous language.

5. DDD building blocks include:
    - Entities: Objects that have a distinct identity that persists over time.
    - Value Objects: Immutable objects that are defined by their attributes.
    - Aggregates: A cluster of domain objects that can be treated as a single unit.
    - Repositories: Mechanisms for storing, retrieving, and searching for objects.
    - Services: Operations that don't naturally belong to an object.

6. Command Query Responsibility Segregation (CQRS) is a pattern that separates read and write operations for a data store. It allows you to scale read and write operations independently and optimize each operation.

7. Event Sourcing is a pattern where state changes are logged as a sequence of events. This allows you to reconstruct the state of an object at any point in time, and it also provides a full audit trail of changes.

8. CQRS use cases include systems with high performance requirements, complex business rules, or where the read and write models are significantly different. Pros of CQRS include improved performance and scalability, and clear separation of concerns. Cons include increased complexity and the need for synchronization between the read and write models.

9. Event Sourcing use cases include systems where auditing is important, where you need to keep a history of state changes, or where you need to analyze state changes over time. Pros of Event Sourcing include full auditability, flexibility in handling state changes, and the ability to reconstruct past states. Cons include complexity in handling events, especially when events can be out of order or in error.

10. To handle external queries in an event-sourced system, you can use a Read Model that is updated by the events in your system. This Read Model can be used to handle queries without affecting the event store. For queries to external systems or APIs, you can use an Anti-Corruption Layer to translate between your model and the external system.

The Gang of Four (GoF) design patterns are categorized into three groups: Creational, Structural, and Behavioral.

1. **Creational Patterns**: These patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. The basic form of object creation could result in design problems or added complexity to the design. Creational design patterns solve this problem by controlling this object creation. Examples include:
    - Singleton: Ensures a class only has one instance, and provides a global point of access to it.
    - Factory: Provides an interface for creating instances of a class, with its subclasses deciding which class to instantiate.
    - Builder: Separates the construction of a complex object from its representation, allowing the same construction process to create various representations.

2. **Structural Patterns**: These patterns deal with object composition or, in other words, they help in answering "How to build a software component?". They are about organizing different classes and objects to form larger structures and provide new functionality. Examples include:
    - Adapter: Allows classes with incompatible interfaces to work together by wrapping its own interface around that of an already existing class.
    - Decorator: Dynamically adds/overrides behaviour in an existing method of an object.
    - Proxy: Provides a surrogate or placeholder for another object to control access to it.

3. **Behavioral Patterns**: These patterns are specifically concerned with communication between objects. They are about identifying common communication patterns between objects and realize these patterns. Examples include:
    - Observer: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
    - Strategy: Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.
    - Command: Encapsulates a request as an object, thereby letting users parameterize clients with queues, requests, and operations.