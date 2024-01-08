# Scope
1. Circuit Breaker: The Circuit Breaker pattern is a design pattern used in modern software development to detect failures and encapsulates the logic of preventing a failure from constantly recurring, during maintenance, temporary external system failure or unexpected system difficulties. It's like an electrical circuit breaker that switches off the current to prevent the wires from overheating when there is too much electricity flowing through them.

2. Retry Strategy: The Retry pattern enables an application to retry an operation in the expectation that it'll succeed. An application can retry an operation if the previous attempt failed due to some temporary issue. This can be useful when the application is trying to connect to a service or network resource.

3. Throttling: Throttling is a process that is used to control the usage of APIs by consumers during a given period. It's a way to limit the usage of resources used by an API. This can be useful in scenarios where you want to limit the number of requests a client can make to an API within a given amount of time.
# Questions
1. What is service reliability? What can go wrong?
2. What is retries? What potential issues retries can bring?
3. How to deal with fallbacks? What service can do to provide response to the user in case there is a fails in communication?
4. Which fallbacks options you know? ( Graceful Degradation, Cache, Functional redundancy, Stubbed data)
5. Timeouts configuration is important for communication? Why?
6. How properly implement retry strategy?
7. What is Circuit breaker pattern and how it works?
8. Should we implement both Circular breaker and Retry strategy?
9. What is throttling pattern? How it helps to increase service reliability?
10. What common throttling strategies you know (Drop requests above value, Prioritize critical traffic, Drop uncommon clients, Limit concurrent requests)
11. How to properly check service reliability and fault tolerance?
# Answers
1. Service reliability is the ability of a system to consistently perform its intended function under normal conditions for a specific period of time. Things that can go wrong include network failures, software bugs, hardware failures, and unexpected load or traffic.

2. Retries are a common technique to handle temporary failures. If a request fails, the client can wait a bit and try again. However, retries can potentially exacerbate the problem if the system is already struggling, leading to a vicious cycle of more failures and retries, known as a retry storm.

3. Fallbacks are a way to provide a degraded level of service when the system is experiencing failures. The goal is to provide the best possible user experience under the circumstances. This could involve returning cached data, default values, or a simplified version of the service.

4. Fallback options include:
    - Graceful Degradation: Continue to function but provide a reduced level of service.
    - Cache: Return cached data if it's available.
    - Functional Redundancy: Switch to a redundant component or service.
    - Stubbed Data: Return hardcoded or stubbed data.

5. Configuring timeouts is important because it prevents the system from waiting indefinitely for a response. This can free up resources and allow the system to handle other requests. However, setting timeouts too short can lead to unnecessary failures, while setting them too long can lead to resource exhaustion.

6. To properly implement a retry strategy, you should:
    - Use exponential backoff: Increase the delay between retries exponentially to avoid overwhelming the system.
    - Set a maximum number of retries: After a certain number of attempts, it's better to fail than to keep trying indefinitely.
    - Consider using jitter: Random variation in the delay can prevent retries from multiple clients from synchronizing and overwhelming the system.

7. The Circuit Breaker pattern is a way to automatically degrade functionality when the system is under stress. It works like an electrical circuit breaker: After a certain number of failures, it "trips" and prevents further operations until a timeout period has passed.

8. Implementing both a Circuit Breaker and Retry strategy can be beneficial. Retries can handle temporary failures, while the Circuit Breaker can prevent the system from being overwhelmed by retries during a prolonged failure.

9. Throttling is a way to limit the rate of requests that a client can make. This can prevent a single client from overwhelming the system. It can be implemented using techniques like token bucket or leaky bucket algorithms.

10. Common throttling strategies include:
- Drop requests above a certain rate: Simply reject any request that exceeds the limit.
- Prioritize critical traffic: Allow more important requests to exceed the limit.
- Drop uncommon clients: If a client is making too many requests, drop their requests first.
- Limit concurrent requests: Only allow a certain number of simultaneous requests.

11. To properly check service reliability and fault tolerance, you can use techniques like monitoring, logging, and alerting to detect failures. You can also use chaos engineering to intentionally introduce failures and observe how the system responds. This can help you identify weaknesses and improve the system's resilience.