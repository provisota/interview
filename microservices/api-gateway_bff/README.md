# API Gateway/BFF (Backend for Frontend)
1. API Gateway Aggregations vs Aggregation Service Pattern:
    - API Gateway Aggregations: In this pattern, the API Gateway takes on the responsibility of aggregating responses from multiple microservices and returning the combined response to the client. This can simplify the client code and reduce the number of round-trip requests between the client and the server. However, it can also increase the complexity of the API Gateway and couple it to the internal structure of the microservices.
    - Aggregation Service Pattern: In this pattern, a separate Aggregation Service is responsible for aggregating data from multiple microservices. This can keep the API Gateway simple and decoupled from the microservices, but it introduces another service that needs to be managed.
    - Cross-cutting concerns: Both patterns need to handle cross-cutting concerns like security and throttling. Security can be handled by implementing authentication and authorization at the API Gateway level. Throttling can be implemented at the API Gateway to protect the microservices from being overwhelmed by too many requests.

2. Frameworks:
    - Kong: An open-source API Gateway and platform that provides features like load balancing, authentication, rate limiting, and more.
    - Nginx: A popular web server that can also be used as a reverse proxy, load balancer, and API Gateway.
    - Ocelot: A .NET API Gateway framework. It provides features like routing, request aggregation, and authentication.
    - Zuul: An edge service in the Netflix OSS stack. It provides dynamic routing, monitoring, resiliency, and security.
    - Ambassador: An open-source API Gateway built on Envoy Proxy, designed specifically for Kubernetes.
    - Spring Cloud API Gateway: A library for building API Gateways on top of Spring MVC, Spring WebFlux, and Project Reactor.
# Questions
1. what is API gateway?
2. when to use API gateway in microservices architecture?
3. describe approaches to handle cross-cutting concerns with API gateway? (service discovery, security, throttling, circuit breaker)
4. describe API gw framework that you had experience with or know?
5. how api gateway can decrease complexity of microservices development?
6. what are downsides of API gateway
7. Describe internal architecture of one of the existing
# Answers
1. An API Gateway is a server that acts as an API front-end, receives API requests, enforces throttling and security policies, passes requests to the back-end service and then passes the response back to the requester. It acts as a reverse proxy to accept all application programming interface (API) calls, aggregate the various services required to fulfill them, and return the appropriate result.

2. An API Gateway is typically used in a microservices architecture to provide a single point of entry for different microservices. It can handle cross-cutting concerns like routing, authentication, and rate limiting, and it can aggregate responses from multiple microservices.

3. Approaches to handle cross-cutting concerns with an API Gateway include:
    - Service Discovery: The API Gateway can use a service registry to discover and route requests to available microservices.
    - Security: The API Gateway can handle authentication and authorization, ensuring that requests are from authenticated and authorized clients.
    - Throttling: The API Gateway can limit the rate of requests to prevent overloading the microservices.
    - Circuit Breaker: The API Gateway can use a circuit breaker to prevent a network or service failure from cascading to other services.

4. Kong is an open-source API Gateway and platform that provides features like load balancing, authentication, rate limiting, and more. It is designed to be easily scalable and modular, with plugins available for many common tasks and integrations.

5. An API Gateway can decrease the complexity of microservices development by providing a single entry point for clients. It can handle cross-cutting concerns, reducing the amount of work that each microservice needs to do. It can also aggregate responses from multiple microservices, simplifying the client code.

6. Downsides of an API Gateway include:
    - It can become a bottleneck if not properly managed and scaled.
    - It can increase the latency of requests because all requests must pass through it.
    - It can be a single point of failure if not properly designed for high availability.

7. The internal architecture of an API Gateway like Kong includes components like a reverse proxy, a plugin system, and a service registry. The reverse proxy routes incoming requests to the appropriate microservice. The plugin system allows adding functionality like authentication, rate limiting, and transformations. The service registry keeps track of the available microservices and their network locations.