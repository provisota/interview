# Distributed Tracing/Logging/Monitoring
1. OpenTracing, Zipkin, Jaeger, AWS X-Ray, ELK (EFK) Stack, Prometheus, Datadog, and Grafana are all tools and protocols used for distributed tracing, logging, and monitoring in microservices architectures:

    - OpenTracing is a vendor-neutral API for distributed tracing. It allows developers to add instrumentation to their applications without binding to any particular tracing system.

    - Zipkin and Jaeger are distributed tracing systems. They help gather timing data needed to troubleshoot latency problems in microservice architectures.

    - AWS X-Ray is a service offered by Amazon Web Services that collects data for requests that an application serves, and provides tools for filtering and aggregating the collected data so you can analyze it.

    - ELK (Elasticsearch, Logstash, Kibana) Stack is a popular open-source log management platform. In the EFK stack, Filebeat (a lightweight log shipper) is used instead of Logstash.

    - Prometheus is an open-source systems monitoring and alerting toolkit. It can handle numeric time series data.

    - Datadog is a monitoring service for cloud-scale applications, bringing together data from servers, databases, tools, and services to present a unified view of an entire stack.

    - Grafana is a multi-platform open-source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources.

2. In a microservices architecture, you should monitor:

    - Performance Metrics: This includes things like response times, throughput, and error rates of your services.

    - System Metrics: This includes CPU usage, memory usage, disk I/O, and network I/O.

    - Business Metrics: These are high-level metrics that may be unique to your application, like the number of user signups or orders placed.

    - Availability: This is the percentage of time your system is operational and available to users.

    - Errors: Any exceptions or errors that occur should be logged and monitored.

   Alerts should be set up to notify you when metrics hit unacceptable levels, such as high error rates, low availability, or performance degradation.
# Questions
1. what is OpenTracing/OpenTelemetry?
2. Describe approaches of logging in distributed systems
3. How to collect logs from application runs on top of Kubernetes
4. How to achieve observability in a distributed system?
5. What is Prometheus/Datadog? How these tools is differs? How they are collecting monitoring information?
6. Describes components of Prometheus stack to provide distributed Monitoring & Alerting
7. Jaeger configuration and practices.
# Answers
1. OpenTracing/OpenTelemetry:
    - OpenTracing is a vendor-neutral API specification for distributed tracing. It allows developers to add instrumentation to their applications without binding to any particular tracing system. This means that you can add tracing to your application once and choose the tracing system later.
    - OpenTelemetry is a set of APIs, libraries, agents, and instrumentation that to observe traces and metrics from your application. It's a CNCF project that has merged the OpenTracing and OpenCensus projects.

2. Logging in Distributed Systems:
    - Centralized Logging: All logs from the various services are sent to a centralized logging service where they can be stored, indexed, and analyzed. This allows you to easily search and correlate logs from different services.
    - Structured Logging: Logs are written in a structured format (like JSON), which makes them easier to analyze programmatically.
    - Contextual Logging: Including context (like trace IDs or tags) in your logs that allows you to correlate logs from the same request or operation.

3. Collecting Logs from Applications Running on Kubernetes:
    - You can use a logging agent that runs on each node in your cluster. The agent is responsible for collecting logs from the applications and sending them to a centralized logging service. Examples of logging agents include Fluentd and Fluent Bit.
    - Kubernetes also provides features like log rotation and retention policies to manage the lifecycle of the logs.

4. Achieving Observability in a Distributed System:
    - Observability in a distributed system can be achieved through a combination of logging, metrics, and tracing. These provide information about the behavior and performance of your system.
    - Logging provides detailed information about what the system is doing, metrics provide quantitative information about the system's performance and behavior, and tracing provides detailed information about request execution across multiple services.

5. Prometheus/Datadog:
    - Prometheus is an open-source systems monitoring and alerting toolkit. It provides a multi-dimensional data model, a flexible query language, and autonomous server nodes. It collects metrics from configured targets at given intervals, evaluates rule expressions, and can trigger alerts if some condition is observed to be true.
    - Datadog is a commercial monitoring service that provides full-stack observability through logs, metrics, and traces. It offers features like anomaly detection, forecasting, and machine learning-based alerts.
    - The main difference between the two is that Prometheus is a pull-based system (it scrapes metrics from monitored systems) while Datadog is a push-based system (metrics are sent to Datadog by the monitored systems).

6. Prometheus Stack Components:
    - Prometheus Server: Collects and stores metrics.
    - Alertmanager: Handles alerts sent by client applications.
    - Pushgateway: Allows ephemeral and batch jobs to expose their metrics to Prometheus.
    - Exporters: Expose metrics in a format that Prometheus can scrape.

7. Jaeger Configuration and Practices:
    - Jaeger is a distributed tracing system. It collects and visualizes traces of your transactions, providing visibility into your system's behavior.
    - Jaeger includes a backend server, a UI, and libraries for instrumenting your code.
    - You can configure Jaeger to sample a certain percentage of traces, to control the amount of data you collect.
    - Jaeger integrates with Kubernetes and can be used with platforms like Istio and Envoy.