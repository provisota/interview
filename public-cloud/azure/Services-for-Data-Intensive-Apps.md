# Services for Data-intensive apps

## Event Hub
Azure Event Hubs is a big data streaming platform and event ingestion service. It can receive and process millions of events per second.

## IoT Hub
Azure IoT Hub is a managed service that acts as a central message hub for bi-directional communication between your IoT application and the devices it manages.

## Data factory
Azure Data Factory is a cloud-based data integration service that allows you to create data-driven workflows for orchestrating and automating data movement and data transformation.

## Stream Analytics
Azure Stream Analytics is a real-time analytics and complex event-processing engine that is designed to analyze and visualize streaming data in real-time.

## Azure Synapse
Azure Synapse Analytics is an integrated analytics service that accelerates time to insight across data warehouses and big data systems. It brings together big data and data warehousing into a single, powerful, and important service.

## Azure Cache for Redis
Azure Cache for Redis provides an in-memory data store based on the open-source software Redis. It improves the performance and scalability of an application that uses back-end data stores heavily.

## Questions
1. What is difference between IoT Hub and Event Hub? Examples?
2. What is purpose of Stream Analytics?
3. What is Azure Synapse Analytics (formerly SQL DW)? MPP
4. What is Azure Cache for Redis and what does it improves?
5. What parts Azure Synapse Analytics workspace consists of?
6. What is Azure Synapse Spark, also known as Spark Pools?

## Answers
1. IoT Hub and Event Hub are both Azure services that handle large amounts of event data, but they are designed for different scenarios. IoT Hub is specifically designed for the Internet of Things scenarios. It supports device-to-cloud and cloud-to-device communication, and enables secure and reliable bi-directional communication between millions of IoT devices and a solution back end. Event Hub, on the other hand, is a big data streaming platform and event ingestion service. It can receive and process millions of events per second, and is often used in log and telemetry data scenarios.

2. Azure Stream Analytics is a real-time analytics service designed to help you analyze and visualize streaming data in real time. It can ingest data from various sources like IoT devices, social media feeds, live feeds, etc., process that data in real time, and output the results to various sinks like databases, dashboards, etc. It's commonly used in scenarios like real-time telemetry analysis, fraud detection, live dashboarding, and more.

3. Azure Synapse Analytics, formerly known as SQL Data Warehouse, is an integrated analytics service that accelerates the delivery of insights from all your data. It brings together big data and data warehousing into a single, powerful, and flexible analytics service. MPP stands for Massively Parallel Processing, a type of computing that uses many separate CPUs running in parallel to execute a program.

4. Azure Cache for Redis is an in-memory data store that is used to power fast, scalable applications. By storing data in memory rather than on disk, Azure Cache for Redis allows applications to access and process the data much faster. It's commonly used to improve the performance of applications by reducing the load on the backend database, and to enable real-time analytics and messaging.

5. Azure Synapse Analytics workspace consists of several parts including on-demand or provisioned resources, integrated security with Azure Active Directory, firewall rules, managed private networks, storage accounts, and more. It also includes features like Synapse Studio for managing, monitoring, and developing analytics, and Synapse pipelines for orchestrating data movement and transformation.

6. Azure Synapse Spark, also known as Spark Pools in Azure Synapse Analytics, is an analytics service that provides a fast, easy, and collaborative Apache Spark-based analytics platform. It allows you to analyze large amounts of data, and build, train, and deploy machine learning models. It's integrated with Azure Synapse Studio, which makes it easy to cleanse, transform, and explore your data before you analyze it.