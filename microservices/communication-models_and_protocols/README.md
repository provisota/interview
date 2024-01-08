# Communication Models and Protocols
1. Communication Models:
    - Synchronous (request-response): In this model, the sender sends a request and waits for a response. The sender cannot continue until it has received the response. This model is simple and straightforward, but it can be inefficient if the sender needs to wait a long time for the response.
    - Asynchronous (event-driven): In this model, the sender sends a request and then continues with other work. When the response arrives, it is handled by an event handler. This model can be more efficient because the sender is not blocked waiting for responses. However, it can be more complex to implement because control is passed between multiple event handlers.

2. Communication Protocols:
    - REST (HTTP1, HTTP/2): REST is an architectural style for designing networked applications. It uses a stateless, client-server communication model, where each request from a client to a server must contain all the information needed to understand and process the request. HTTP1 and HTTP2 are versions of the HTTP protocol used by REST. HTTP2 introduces several improvements over HTTP1, such as multiplexing (multiple requests/responses can be sent over a single TCP connection), server push (the server can send resources to the client proactively), and header compression (reduces overhead).
    - GraphQL: GraphQL is a query language for APIs and a runtime for executing those queries with your existing data. Unlike REST, which has multiple endpoints each returning a fixed data structure, GraphQL has a single endpoint and returns flexible data structures.
    - gRPC: gRPC is a high-performance, open-source framework developed by Google. It uses Protocol Buffers as its interface definition language, allowing developers to define services and message types in .proto files, which can then be compiled into various languages. gRPC supports multiple programming languages, making it an excellent choice for multi-language systems.

3. Binary Serialization Protocols:
    - Protobuf: Protocol Buffers (Protobuf) is a binary serialization protocol developed by Google. It is language-neutral and platform-neutral. It provides a mechanism for serializing structured data, like XML, but smaller, faster, and simpler.
    - Avro: Avro is a binary serialization protocol developed by Apache. It is language-neutral and platform-neutral. Unlike Protobuf, Avro schemas are not required to read or write data, which makes it more dynamic.
    - Thrift: Thrift is a binary serialization protocol developed by Apache. It includes a complete stack for creating clients and servers. The top part is a code generation tool for creating services that communicate seamlessly across programming languages.
    - MessagePack: MessagePack is an efficient binary serialization format. It lets you exchange data among multiple languages like JSON, but it is faster and smaller.
# Questions
1. communication modes
2. describe sync communication models? Pros and cons?
3. describe async communication model with pros and cons?
4. when do you choose sync over async and vice versa?
5. gRPC streams
6. communication protocols
7. describe what communication approach you would use for microservices and why? (rest vs grpc vs graphql)
8. Is GraphQL useless in the HTTP/2 -HTTP/3 era?
9. Compare REST vs gRPC
10. serialization protocols
11. what are capabilities of protobuf, describe use cases
12. what is avro, what it's internal structure, where does it stores schema?
13. compare schema evolution options of protobuf/avro/thrift/message pack
# Answers
1. Communication modes refer to the ways in which systems communicate with each other. This can be synchronous (where the sender waits for a response before continuing) or asynchronous (where the sender continues processing without waiting for a response).

2. Synchronous communication model is a mode of communication where the sender sends a request and waits for a response before continuing. The advantage of this model is its simplicity, as the flow of control is straightforward to understand and manage. However, the downside is that the sender can be blocked for a significant amount of time waiting for the response, which can lead to inefficiency, especially in a distributed system where network latency is a factor.

3. Asynchronous communication model is a mode of communication where the sender sends a request and then continues with other work. When the response arrives, it is handled by an event handler. This model can be more efficient because the sender is not blocked waiting for responses. However, it can be more complex to implement and reason about, because control is passed between multiple event handlers.

4. The choice between synchronous and asynchronous communication often depends on the specific requirements of your application. If you need to wait for a response before you can continue processing, then synchronous communication might be appropriate. However, if you want to improve efficiency by doing other work while waiting for a response, then asynchronous communication might be a better choice.

5. gRPC streams refer to a feature of gRPC that allows clients and servers to send a stream of messages within a single RPC call. There are four types of gRPC streaming: unary (single request, single response), server-side (single request, stream of responses), client-side (stream of requests, single response), and bidirectional (stream of requests, stream of responses).

6. Communication protocols define the rules for how data is transmitted and received in a network. Examples include HTTP/1.1, HTTP/2, gRPC, and GraphQL.

7. The choice of communication approach for microservices depends on the specific needs of your application. REST is simple and widely adopted, but it can be verbose and require multiple round trips to fetch related resources. gRPC is efficient and supports streaming, but it requires HTTP/2 and is not as human-readable as REST. GraphQL allows clients to request exactly the data they need, reducing over-fetching, but it has a learning curve and can be complex to set up.

8. GraphQL is not useless in the HTTP/2 - HTTP/3 era. While HTTP/2 and HTTP/3 provide improvements like multiplexing and header compression that can make REST more efficient, GraphQL still has the advantage of allowing clients to specify exactly what data they need. This can reduce over-fetching and improve efficiency, especially for complex queries with multiple related resources.

9. REST and gRPC are both communication protocols, but they have some key differences. REST is based on standard HTTP methods and status codes, and it uses JSON for data representation. It's simple, widely adopted, and human-readable. gRPC, on the other hand, is a high-performance protocol that uses Protocol Buffers for data representation. It supports streaming, requires HTTP/2, and is not as human-readable as REST.

10. Serialization protocols are used to convert data structures or object states into a format that can be stored or transmitted and reconstructed later. Examples include Protocol Buffers, Avro, Thrift, and MessagePack.

11. Protocol Buffers (protobuf) is a binary serialization protocol developed by Google. It's language-neutral, platform-neutral, and provides a mechanism for serializing structured data. It's smaller, faster, and simpler than XML. Use cases for protobuf include data storage, communication protocols, and data interchange formats.

12. Avro is a binary serialization protocol developed by Apache. Unlike Protobuf, Avro schemas are not required to read or write data, which makes it more dynamic. Avro stores schemas in JSON format, making it more readable. The schema is stored in the data file, and Avro libraries know how to serialize and deserialize data based on the schema.

13. Schema evolution in serialization protocols refers to the ability to modify the schema over time, while ensuring compatibility with older versions of the schema. Protobuf supports adding new fields and marking fields as optional. Avro supports adding, removing, or modifying fields with a default value. Thrift supports adding new fields, but removing or modifying existing fields can break compatibility. MessagePack doesn't support schema evolution directly, but you can implement it at the application level.