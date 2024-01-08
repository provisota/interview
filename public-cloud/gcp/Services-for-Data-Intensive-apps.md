# Services for Data-intensive apps
Google Cloud Platform provides a suite of services designed to help you handle data-intensive tasks. These include Dataflow and Dataprep for data processing, Cloud Composer for workflow orchestration, Google Data Studio for data visualization, BigQuery for big data analytics, and IoT Core for managing IoT devices.

# Cloud Composer
Cloud Composer is a fully managed workflow orchestration service that empowers you to author, schedule, and monitor pipelines that span across clouds and on-premises data centers.

# Dataflow/Dataprep
Dataflow is a fully managed service for transforming and enriching data in stream (real time) and batch (historical) modes with equal reliability and expressiveness. Dataprep by Trifacta is an intelligent data service for visually exploring, cleaning, and preparing structured and unstructured data for analysis.

# BigQuery
BigQuery is Google's fully managed, NoOps, low-cost analytics database. With BigQuery you can query terabytes and terabytes of data without having any infrastructure to manage or needing a database administrator.

# BigQuery BI
BigQuery BI Engine is a fast, in-memory analysis service. With BI Engine you can empower your analysts to perform highly interactive analysis on large datasets.

# Data Studio
Data Studio is Google's report and dashboard creation tool. It's easy to connect to your data sources, visualize data, and share it with your team or the world.

# Cloud Datalab
Cloud Datalab is a powerful interactive tool created to explore, analyze, transform, and visualize data and build machine learning models on Google Cloud Platform.

# Data Fusion
Data Fusion is a fully managed, cloud-native, enterprise data integration service for quickly building and managing data pipelines. It provides a graphical interface to increase ease of use and productivity.

# IOT core
Cloud IoT Core is a fully managed service that allows you to easily and securely connect, manage, and ingest data from millions of globally dispersed devices.

# Questions
1. What are the differences between Dataflow and Dataprep?
2. What are use cases for Cloud Composer?
3. What is Google Data Studio?
4. What are slots in BigQuery? How does BigQuery query data?
5. What table partitioning/clustering options does BigQuery provide?
6. What are schema evolution options in BigQuery?
7. How to migrate BigQuery table schemas cost efficiently?
8. Describe main components and flows of IoT Core.
9. How to organize edge computing with IoT Core?

# Answers
1. Dataflow is a fully managed service for executing Apache Beam pipelines within Google Cloud. It's designed for large-scale, complex data transformation tasks. Dataprep, on the other hand, is an intelligent cloud data service for visually exploring, cleaning, and preparing data for analysis.

2. Cloud Composer is a fully managed workflow orchestration service built on Apache Airflow. Use cases include data transformation, data movement, automating infrastructure, and machine learning pipelines.

3. Google Data Studio is a reporting tool for business intelligence that allows you to visualize your data through highly configurable charts and tables.

4. In BigQuery, slots are the basic units of computational capacity. When you run a query, BigQuery uses these slots to execute it. BigQuery queries data using a columnar storage structure and a tree architecture for aggregation.

5. BigQuery provides table partitioning and clustering to optimize the performance of your queries and reduce costs. Partitioning divides your table into segments, while clustering sorts your data based on the values in certain columns.

6. Schema evolution in BigQuery allows you to modify the schema of your tables over time. You can add new columns, relax required columns, and make other changes without downtime.

7. To migrate BigQuery table schemas cost efficiently, you can use the BigQuery Data Transfer Service, which automates the movement of data between BigQuery and external data sources.

8. IoT Core is a fully managed service for connecting, managing, and ingesting data from IoT devices. It consists of two main components: a device manager for registering devices and a protocol bridge for connecting devices to Google Cloud.

9. To organize edge computing with IoT Core, you can use Cloud IoT Edge, which extends Google Cloud's powerful data processing and machine learning capabilities to IoT gateways and end devices.