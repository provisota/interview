# Services for Data-Intensive apps
1. **IoT Architecture and Components**: IoT (Internet of Things) architecture refers to the system of numerous elements: sensors, protocols, actuators, cloud services, and layers that make up the IoT ecosystem. The key components of IoT architecture include:

    - **Devices**: These are the physical objects that are connected to the IoT network. They can be anything from a simple sensor to a complex machine like a car.

    - **Gateways and Data Acquisition Systems**: These are the intermediaries between the devices and the cloud. They collect data from the devices and send it to the cloud.

    - **Edge IT Systems**: These are the systems that process the data before it is sent to the cloud. They can perform tasks like data filtering, security checks, and more.

    - **Data Centers and Cloud**: This is where the data is stored and processed. It can be a physical data center or a cloud-based platform.

    - **Applications**: These are the end-user applications that use the processed data to provide useful insights or actions.

2. **Athena, Redshift, Glue, QuickSight**:

    - **Athena**: Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is serverless, so there is no infrastructure to manage, and you pay only for the queries that you run.

    - **Redshift**: Amazon Redshift is a fast, scalable data warehouse that makes it simple and cost-effective to analyze all your data across your data warehouse and data lake. Redshift delivers faster performance than other data warehouses by using machine learning, massively parallel query execution, and columnar storage on high-performance disk.

    - **Glue**: AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for users to prepare and load their data for analytics. You can create and run an ETL job with a few clicks in the AWS Management Console.

    - **QuickSight**: Amazon QuickSight is a fast, cloud-powered business intelligence service that makes it easy to deliver insights to everyone in your organization. QuickSight lets you create and publish interactive dashboards that can be accessed from browsers or mobile devices.

3. **Edge Computing**: Edge computing is a distributed computing paradigm that brings computation and data storage closer to the location where it is needed, to improve response times and save bandwidth. In the context of IoT, edge computing can be used to process data from IoT devices in real-time, reducing the need for long round trips to the cloud. This can be particularly useful for applications that require real-time processing and analytics.
# Questions
1. How to achieve High IO networking between EC2 instances for data intensive distributed systems?
2. How you will design ETL processing on AWS?
3. Describe IoT platform components and integration?
4. AWS Glue: supported data formats, internal architecture, what is crawler, job, data catalog?
5. GreenGrass, Edge computing?
# Answers
1. High IO networking between EC2 instances can be achieved by using Amazon's Elastic Network Adapter (ENA) which supports up to 100 Gbps of bandwidth. Placement groups are another feature that can be used to influence the networking performance. A placement group is a logical grouping of instances within a single Availability Zone. Using placement groups can enable applications to participate in a low-latency, 100 Gbps network. Enhanced Networking should be enabled to get the maximum performance.

2. ETL processing on AWS can be designed using AWS Glue. AWS Glue is a fully managed ETL service that makes it easy to move data between data stores. AWS Glue simplifies and automates the difficult and time-consuming tasks of data discovery, conversion mapping, and job scheduling. AWS Glue crawlers connect to your source or target data store, progresses through a prioritized list of classifiers to determine the schema for your data, and then creates metadata in the AWS Glue Data Catalog.

3. IoT platform components include devices, gateways and data acquisition systems, edge IT systems, data centers and cloud, and applications. Devices are the physical objects connected to the IoT network. Gateways and data acquisition systems act as intermediaries between the devices and the cloud. Edge IT systems process the data before it is sent to the cloud. Data centers and cloud is where the data is stored and processed. Applications are the end-user applications that use the processed data.

4. AWS Glue supports various data formats like CSV, JSON, XML, Avro, and relational databases. The internal architecture of AWS Glue consists of a central metadata repository known as the AWS Glue Data Catalog, an ETL engine that automatically generates Python or Scala code, and a flexible scheduler that handles dependency resolution, job monitoring, and retries. A crawler in AWS Glue connects to a data store, extracts metadata and creates table definitions in the Data Catalog. A job is the business logic that performs the ETL work. The Data Catalog is a central metadata repository that is persistently stored.

5. AWS Greengrass is software that lets you run local compute, messaging, data caching, sync, and ML inference capabilities for connected devices in a secure way. With AWS Greengrass, connected devices can run AWS Lambda functions, keep device data in sync, and communicate with other devices securely even when not connected to the Internet. Edge computing refers to the need to perform data processing at or near the source of data generation. This is needed in locations that have limited connectivity to the cloud. AWS Greengrass is a service that extends AWS to edge devices so they can act locally on the data they generate, while still using the cloud for management, analytics, and durable storage.