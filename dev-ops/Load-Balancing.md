# Load Balancing
Load balancing is a technique used to distribute network traffic across multiple servers. This ensures no single server bears too much demand, thereby increasing the reliability and availability of applications, minimizing response time, and ensuring optimal resource utilization.

There are several types of load balancing, including:

1. **Round Robin**: This is one of the simplest methods for distributing client requests across a group of servers. When a request comes in, the load balancer forwards the request to the next server in the list. The load balancer continues to distribute incoming requests to the server in the circular order, looping back to the first server when it reaches the end of the list.

2. **Least Connections**: This method directs traffic to the server with the fewest active connections. This approach can be more efficient than round-robin if the servers have different processing capabilities.

3. **IP Hash**: The IP address of the client is used to determine which server receives the request. This can be useful for ensuring a client consistently connects to the same server.

4. **Least Response Time**: This method directs traffic to the server with the fewest active connections and the lowest average response time.

5. **URL Hash**: The URL or another characteristic of the HTTP request is used to determine the server that will receive the request.

6. **Weighted Distribution**: With this method, the administrator assigns a weight to each server based on its traffic-handling capacity. The one with higher weightage gets more requests.

In addition to these, there are more advanced load balancing methods that take into account server performance, the content type of the traffic, and other factors. The choice of load balancing method depends on the specific requirements of your application.
# Questions
1. What is load balancing?
2. Which tools do you know which allow to load balance http traffic?
3. Which types of load balancers do you know? (layer 4 vs layer 7)
4. Global load balancers
# Answers
1. Load balancing is a technique used to distribute network traffic across multiple servers. This ensures no single server bears too much demand, thereby increasing the reliability and availability of applications, minimizing response time, and ensuring optimal resource utilization.

2. There are several tools that can be used to load balance HTTP traffic, including:
    - Nginx: An open-source web server that can also be used as a reverse proxy and load balancer.
    - HAProxy: A free, very fast, and reliable solution offering high availability, load balancing, and proxying for TCP and HTTP-based applications.
    - AWS Elastic Load Balancer (ELB): A cloud-based load balancer service provided by Amazon Web Services (AWS).
    - Google Cloud Load Balancer: A fully distributed, software-defined, managed service for all your load balancing needs on Google Cloud.
    - Azure Load Balancer: A built-in load balancing service for Microsoft Azure.

3. There are two main types of load balancers:
    - Layer 4 Load Balancer (Transport Layer): This operates at the transport layer of the OSI model. It decides where to send new connections based on IP range, hashing, or least connection count.
    - Layer 7 Load Balancer (Application Layer): This operates at the highest level of the OSI model. It makes routing decisions based on attributes of the HTTP header, the client's IP address, the resource's URI, or even the cookie parameters.

4. Global load balancers distribute traffic across multiple servers located in different geographical locations. They are designed to improve application availability and responsiveness and are crucial for multinational organizations. Examples include AWS Route 53, Google Cloud's Global Load Balancer, and Azure Traffic Manager.