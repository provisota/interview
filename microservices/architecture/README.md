# Architecture
1. Microservices vs SOA:
    - Microservices and Service-Oriented Architecture (SOA) are both architectural styles that structure an application as a collection of services. However, they differ in scope and operations. Microservices are small, independent services that work together, while SOA is an architectural style that allows services to communicate over a network.
    - Pros of Microservices: Independent deployment, technology diversity, fault isolation, scalability, and organizational alignment.
    - Cons of Microservices: Distributed system complexity, operational overhead, network latency, data consistency, and increased memory footprint.
    - Pros of SOA: Business agility, reusability, scalability, and easier integration.
    - Cons of SOA: Complexity, requires a higher level of coordination, and can lead to information bottlenecks.

2. When to split Microservices:
    - It's often beneficial to split a monolithic application into microservices when the application becomes too large and complex to manage effectively. Other reasons might include the need for different services to use different data storage technologies, the need to scale services independently, or the need to isolate services that require a high level of security.

3. DDD in Microservices:
    - Domain-Driven Design (DDD) is an approach to software development that centers the development on programming a domain model that has a rich understanding of the processes and rules of a domain. The goal of DDD is to create a software model that is a true reflection of the underlying business domain. In the context of microservices, DDD can help in designing and defining the boundaries of each microservice based on bounded contexts.

4. Scaling Microservices:
    - Microservices can be scaled horizontally (by running more instances of the microservice) or vertically (by adding more resources such as CPU or memory to the machine where the microservice is running). Horizontal scaling is often preferred because it allows each instance to remain small and efficient, while still increasing the capacity of the overall application.
# Questions
1. what is microservice?
2. how to decide what part of code to consider a microservice?
3. what are pros and cons of microservices?
4. when do you usually consider splitting monolithic app to microservices?
5. describe approaches to handle cross-cutting concerns in microservices?
6. what are typical microservice related patterns?
7. describe patterns of decomposition of monolithic application
# Answers
1. A microservice is an architectural style that structures an application as a collection of small autonomous services, modeled around a business domain. Each microservice runs in its own process and communicates with others using protocols such as HTTP/REST or messaging. Each microservice can be deployed, upgraded, scaled, and restarted independently of other services in the application.

2. Deciding what part of the code to consider as a microservice often involves identifying bounded contexts within your application. A bounded context is a specific responsibility that corresponds to a certain business capability. It's often beneficial to align microservices with these bounded contexts. You can also consider factors like the rate of change, the need for scalability, and the team organization.

3. Pros of Microservices:
    - Independent deployment: Each microservice can be deployed independently of others.
    - Technology diversity: Different microservices can use different technologies.
    - Fault isolation: Failure in one microservice doesn't affect others.
    - Scalability: Each microservice can be scaled independently based on its needs.
    - Organizational alignment: Microservices can align with specific teams or business capabilities.

   Cons of Microservices:
    - Distributed system complexity: Microservices introduce complexity of managing a distributed system.
    - Operational overhead: Each microservice might need to be monitored and managed independently.
    - Network latency: Communication between microservices can introduce network latency.
    - Data consistency: Ensuring data consistency across microservices can be challenging.
    - Increased memory footprint: Each microservice runs in its own process, which can lead to higher memory consumption.

4. It's often beneficial to split a monolithic application into microservices when the application becomes too large and complex to manage effectively. Other reasons might include the need for different services to use different data storage technologies, the need to scale services independently, or the need to isolate services that require a high level of security.

5. Cross-cutting concerns in microservices can be handled using various approaches. For example, you can use an API Gateway to handle concerns like request routing, composition, and security. You can use centralized logging and monitoring services to collect and analyze logs and metrics from all microservices. You can also use distributed tracing tools to track requests as they flow through the system.

6. Typical microservice-related patterns include:
    - API Gateway: A server that acts as an API front-end, receives API requests, enforces throttling and security policies, passes requests to the back-end service and then passes the response back to the requester.
    - Circuit Breaker: A design pattern used in modern software development to detect failures and encapsulates the logic of preventing a failure from constantly recurring.
    - Saga: A design pattern that provides a way to define a series of local transactions that can be executed in a distributed environment.
    - Service Registry: A database of services, their instances and their locations. Service instances get registered with the service registry on startup and deregistered on shutdown.

7. Patterns of decomposition of a monolithic application include:
    - Decompose by business capability: This involves identifying the different business capabilities within your application and creating a microservice for each one.
    - Decompose by subdomain: This involves identifying the different subdomains within your application and creating a microservice for each one. This is often done using Domain-Driven Design (DDD).
    - Strangler Fig pattern: This involves gradually extracting parts of a monolithic application and moving them to separate services while the monolith is still in operation.