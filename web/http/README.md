# Scope
1. HTTP (Hypertext Transfer Protocol) is a protocol used for transmitting hypertext requests and information between servers and browsers. Here are some key components:

    - Request: An HTTP request is made by a client (usually a web browser) to a server. It includes a method (GET, POST, PUT, DELETE, etc.), a URL, headers, and sometimes a body.

    - Response: An HTTP response is what is sent by a server to a client in response to an HTTP request. It includes a status code, headers, and a body.

    - Methods: HTTP methods include GET (retrieve), POST (send data), PUT (update data), DELETE (remove data), and others.

    - Headers: HTTP headers let the client and the server pass additional information with an HTTP request or response. They define the operating parameters of an HTTP transaction.

    - Status Codes: HTTP status codes are issued by a server in response to a client's request. They include 200 (OK), 404 (Not Found), 500 (Internal Server Error), and others.

    - Cookies: HTTP cookies are small pieces of data stored on the user's computer by the web browser. They are used for session management, personalization, and tracking.

2. HTTP1 vs HTTP2:

    - HTTP1: This is the original version of HTTP. It is simple and easy to use, but it has some limitations. For example, it opens a new TCP connection for each request/response, which can be inefficient.

    - HTTP2: This is the latest version of HTTP. It introduces several improvements over HTTP1, such as multiplexing (multiple requests/responses can be sent over a single TCP connection), server push (the server can send resources to the client proactively), and header compression (reduces overhead). These improvements make HTTP2 more efficient and faster than HTTP1.
# Questions
1. Describe what happens when you open webpage in a browser?
2. What is request/response structure?
3. Which HTTP method will be used?
4. Do you know any other HTTP methods?
5. Which groups of status codes do you know?
6. What (usually) happens in case of unexpected server error?
7. Explain the authentication flow using cookies.
8. Key differences between HTTP1.1 and HTTP2?
# Answers
1. When you open a webpage in a browser, the following steps occur:
    - The browser parses the URL to find the protocol, host, port, and path.
    - It forms an HTTP request (or a different request, depending on the protocol).
    - The browser sends the request to the server specified in the URL.
    - The server handles the request and sends back a response.
    - The browser processes the response and renders the page content on the screen.

2. An HTTP request/response structure consists of:
    - Request: A request line (method, URL, and HTTP version), headers, and an optional body.
    - Response: A status line (HTTP version, status code, and status text), headers, and an optional body.

3. The HTTP method used depends on the action being performed. For loading a webpage, the GET method is typically used.

4. Other HTTP methods include POST (send data), PUT (update data), DELETE (remove data), HEAD (retrieve headers), OPTIONS (retrieve supported methods), PATCH (apply partial modifications), and others.

5. HTTP status codes are grouped into five classes:
    - 1xx (Informational): The request was received, and the process is continuing.
    - 2xx (Successful): The request was successfully received, understood, and accepted.
    - 3xx (Redirection): Further action must be taken to complete the request.
    - 4xx (Client Error): The request contains bad syntax or cannot be fulfilled.
    - 5xx (Server Error): The server failed to fulfill an apparently valid request.

6. In case of an unexpected server error (5xx status codes), the server failed to fulfill the request. This could be due to an issue with the server itself or the application running on the server. The specific error message can provide more details about the problem.

7. The authentication flow using cookies typically works as follows:
    - The user provides their credentials (like a username and password).
    - The server verifies the credentials and creates a session for the user.
    - The server sends a Set-Cookie header in the response with a session ID.
    - The browser stores the cookie and sends it with subsequent requests.
    - The server checks the session ID in the cookie to identify the user and maintain the session.

8. The key differences between HTTP1.1 and HTTP2 are:
   - Multiplexing: HTTP2 can send multiple requests for data in parallel over a single TCP connection. This is the most advanced feature and it resolves the problem of "head-of-line blocking" that HTTP1.1 has.
   - Server Push: In HTTP2, server can send resources to the client proactively, rather than waiting for the client to request each one. This can improve performance.
   - Binary Protocol: HTTP2 uses binary protocols that lead to more efficient parsing of messages.
   - Header Compression: HTTP2 uses HPACK compression, which reduces overhead. Many headers are sent with almost every request in HTTP1.1. HTTP2 compresses these headers.
   - Use of one connection: HTTP2 uses only one connection to load a website, and all web assets are downloaded in parallel over this single connection. This is more efficient than HTTP1.1, which opens a new connection for each request.
   - Prioritization: Requests are assigned dependency levels that the server can use to deliver higher priority resources faster. This is a feature that HTTP1.1 lacks.