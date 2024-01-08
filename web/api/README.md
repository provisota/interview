# Scope
1. REST (Representational State Transfer) is an architectural style for designing networked applications. It uses a stateless, client-server communication model, where each request from a client to a server must contain all the information needed to understand and process the request. OpenAPI (formerly known as Swagger) is a specification for building APIs in REST. It provides a way to describe the structure of APIs so that machines can read them. The benefits of using OpenAPI include improved API documentation, generation of client SDKs, and server stubs.
2. gRPC is a high-performance, open-source framework developed by Google. It uses Protocol Buffers as its interface definition language, allowing developers to define services and message types in .proto files, which can then be compiled into various languages. gRPC supports multiple programming languages, making it an excellent choice for multi-language systems. It also supports both unary and streaming communication and has features like authentication, load balancing, and more.
3. GraphQL is a query language for APIs and a runtime for executing those queries with your existing data. Unlike REST, which has multiple endpoints each returning a fixed data structure, GraphQL has a single endpoint and returns flexible data structures. This allows clients to request exactly the data they need, reducing the amount of data that needs to be transferred over the network and improving performance.
4. An API Gateway is a server that acts as an API front-end, receives API requests, enforces throttling and security policies, passes requests to the back-end service and then passes the response back to the requester. It acts as a reverse proxy to accept all application programming interface (API) calls, aggregate the various services required to fulfill them, and return the appropriate result. It reduces the number of requests/roundtrips, simplifies the client code, and improves performance. Examples of API Gateways include Amazon API Gateway, Kong, and Apigee.
# Questions
1. What is REST?
2. Describe REST API  principles.
3. What is the difference between POST, PUT and PATCH methods semantic in RESTful APIs?
4. Which approaches to REST API versioning do you know? Can you compare them?
5. Which approaches to REST API pagination do you know? Can you compare them?
6. How do you document REST API?
7. Which types of gRPC service method do you know? (e.g. unary RPC, server streaming, client streaming, bidirectional streaming).
8. How do you evolve gRPC API in a backward/forward compatible way?
9. What is gRPC deadline?
10. How do you modify data with GraphQL?
11. What is the purpose of API gateway?
12. What is the purpose of hypermedia in REST? What is HATEOAS?
13. Compare REST with gRPC and GraphQL. Pros/cons and when to use them?
# Answers
1. REST (Representational State Transfer) is an architectural style for designing networked applications. It uses a stateless, client-server communication model, where each request from a client to a server must contain all the information needed to understand and process the request.

2. REST API principles include:
    - Client-Server: The client and server are separate entities that communicate over a network. The client is responsible for the user interface and user experience, and the server is responsible for processing requests and managing resources.
    - Stateless: Each request from a client to a server must contain all the information needed to understand and process the request. The server should not store anything about the latest HTTP request the client made.
    - Cacheable: Responses from the server can be cached by the client. This can improve performance by reducing the load on the server and the network.
    - Uniform Interface: The method of communication between a client and a server must be uniform and consistent.

3. In RESTful APIs:
    - POST is used to create a new resource.
    - PUT is used to update an existing resource or create it if it doesn't exist.
    - PATCH is used to partially update an existing resource.

4. Approaches to REST API versioning include:
    - URI Versioning: The version number is included in the URI (e.g., /v1/posts).
    - Query Parameter Versioning: The version number is included in the query parameters (e.g., /posts?version=1).
    - Header Versioning: The version number is included in the headers of the request.
      Each approach has its pros and cons, and the choice depends on the specific requirements of the API.

5. Approaches to REST API pagination include:
    - Offset-based pagination: The client specifies the number of items to skip before starting to return entries (e.g., /posts?offset=25&limit=10).
    - Cursor-based pagination: The client is provided a cursor which points to a specific item in the list. The server returns the cursor for the client to use in subsequent requests (e.g., /posts?cursor=abcd1234&limit=10).
      Offset-based pagination is simple to implement but can have performance issues with large datasets. Cursor-based pagination can provide better performance but is more complex to implement.

6. REST APIs can be documented using specifications like OpenAPI (formerly Swagger). This provides a way to describe the structure of APIs so that machines can read them. The benefits of using OpenAPI include improved API documentation, generation of client SDKs, and server stubs.

7. gRPC supports four types of service methods:
    - Unary RPC: A single request followed by a single response.
    - Server streaming RPC: A single request followed by a stream of responses.
    - Client streaming RPC: A stream of requests followed by a single response.
    - Bidirectional streaming RPC: A stream of requests followed by a stream of responses.

8. gRPC APIs can be evolved in a backward/forward compatible way by following certain rules. For example, you should not change the field numbers for any existing fields. You can add new fields, and old servers will simply ignore them. Similarly, you can remove fields, and old clients will just ignore them.

9. gRPC deadline is a time limit for requests. If the server cannot complete the operation in the specified time, the server can cancel the operation and return an error.

10. In GraphQL, you modify data using mutations. A mutation can create, update, or delete data.

11. An API Gateway is a server that acts as an API front-end, receives API requests, enforces throttling and security policies, passes requests to the back-end service and then passes the response back to the requester. It acts as a reverse proxy to accept all application programming interface (API) calls, aggregate the various services required to fulfill them, and return the appropriate result.

12. Hypermedia in REST (HATEOAS, or Hypermedia as the Engine of Application State) is a principle that allows a client to interact with a server entirely through hypermedia provided dynamically by application servers. A REST client needs no prior knowledge about how to interact with an application or server beyond a generic understanding of hypermedia.

13. REST, gRPC, and GraphQL each have their pros and cons:
- REST is simple and uses HTTP methods intuitively, but it can be verbose and require multiple round trips to fetch related resources.
- gRPC is efficient and highly performant, and it supports streaming data, but it requires HTTP/2 and is not as human-readable as REST.
- GraphQL allows clients to request exactly the data they need, reducing over-fetching, but it has a learning curve and can be complex to set up.
  The choice between them depends on the specific requirements of your application.
