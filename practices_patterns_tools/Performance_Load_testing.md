# Performance testing
Performance, Load, and Stress testing are types of testing that are used to understand the behavior of the system under a particular load.

1. **Performance Testing**: This type of testing is done to evaluate the speed, responsiveness, and stability of a system under a particular workload. It is generally done by the testing team. It includes generating a series of tests to investigate the behavior of the system under review under significant load.

2. **Load Testing**: This is a type of performance testing conducted to evaluate the behavior of a system at increasing workload. The workload is increased gradually from normal to many times the actual load. The goal is to identify the maximum operating capacity of an application and to ensure that the application performs satisfactorily when it is subjected to the workload for which it was designed.

3. **Stress Testing**: This involves testing an application under extreme workloads to see how it handles high traffic or data processing. The objective is to identify the breaking point of an application. This test will determine if the application will perform sufficiently if the current load goes well above the expected maximum.

These types of testing can help to identify performance bottlenecks in the system and can ensure that the system can handle high load and stress conditions. They are crucial in ensuring that the system will perform well under production conditions.
# Questions
1. What is performance testing?
2. What are common best practices and pitfalls when doing performance tests?
3. What is Load Testing?
4. What is Stress Testing?
5. What problems Performance / Load / Stress testing trying to find & solve?
# Answers
1. Performance Testing: Performance testing is a type of testing that is performed to determine how a system performs in terms of responsiveness and stability under a particular workload. It can also serve to investigate, measure, validate or verify other quality attributes of the system, such as scalability, reliability and resource usage.

2. Best Practices and Pitfalls in Performance Testing:
    - **Best Practices**:
        - Define clear performance goals: Before starting performance testing, it's important to have clear goals in terms of response times, throughput, and resource utilization.
        - Use realistic workloads: The test workload should be as close as possible to the expected production workload.
        - Monitor system resources: During performance testing, monitor system resources like CPU, memory, disk I/O, and network utilization to identify bottlenecks.
    - **Pitfalls**:
        - Avoid making assumptions: Don't assume that performance in a test environment will be the same as in production. Always validate assumptions with actual data.
        - Don't overlook the end-user experience: High server-side performance doesn't always translate to a good end-user experience. Always consider the impact of performance on the user.

3. Load Testing: Load testing is a type of performance testing that checks how the system operates under an expected load. The goal is to identify performance bottlenecks before the software application goes live.

4. Stress Testing: Stress testing is a type of performance testing that checks the robustness of the system by testing it beyond its maximum operating capacity. The goal is to identify the breaking point of the system and ensure that it fails gracefully.

5. Performance / Load / Stress testing are used to identify and solve problems such as:
    - Performance bottlenecks: These are parts of the system that significantly degrade its performance. Identifying and fixing bottlenecks can greatly improve system performance.
    - System capacity: These tests can help determine the maximum operating capacity of the system, which can be useful for capacity planning.
    - System robustness: Stress testing can help identify whether the system will operate correctly under extreme conditions.