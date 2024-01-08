# Storages & Databases

## Azure Storage
Azure Storage is a Microsoft-managed service providing cloud storage that is highly available, secure, durable, scalable, and redundant. It includes services like Blob Storage, Queue Storage, File Storage, and Table Storage.

## Blobs
Azure Blob Storage is a service for storing large amounts of unstructured object data, such as text or binary data. It can be used for serving images or documents directly to a browser, storing files for distributed access, streaming video and audio, and more.

## Disks
Azure Disks are block-level storage volumes that are managed by Azure and used with Azure Virtual Machines. They come in many different sizes and performance levels, from SSDs to traditional spinning HDDs.

## Files
Azure Files offers fully managed file shares in the cloud that are accessible via the industry standard Server Message Block (SMB) protocol. Azure file shares can be used to replace or supplement on-premises file servers or NAS devices.

## Tables
Azure Table Storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.

## Azure SQL
Azure SQL Database is a fully managed platform as a service (PaaS) database engine that handles most of the database management functions such as upgrading, patching, backups, and monitoring without user involvement.

## Optimizing Azure SQL for workloads
Optimizing Azure SQL for workloads can be achieved by selecting the right service tier and compute size, implementing indexing strategies, and optimizing query performance.

## CosmosDB
Azure Cosmos DB is a globally distributed, multi-model database service for managing data at planet-scale. It supports document, key-value, wide-column, and graph databases and is great for building highly responsive and always-on services.

## Questions
1. What are the types of binary storage in Azure? What are the scenarios for their usage?
2. What is the typical scenario for Table Storage? When to use it and when NOT to use it?
3. What are the typical scenarios for Azure SQL Database?
4. What is Azure SQL Elastic Pool?
5. What is Azure SQL Managed Instance?
6. What are the types of storage in terms of availability (LRS, ZRS, GRS)?
7. How to increase IOPS for a VM that hosts disk-intensive application?
8. How to implement a file share accessible from Azure and on-prem in a hybrid environment?
9. How to choose between Azure SQL Database, Managed Instance, and SQL Server in VM?
10. How to implement HA on each of them?
11. What is CosmosDB? How is it different from Azure SQL?
12. What are available drivers to connect to CosmosDB?
13. How to scale CosmosDB?

## Answers
1. Azure provides several types of binary storage including Blob Storage for unstructured data, Disk Storage for persistent storage of data for VMs, and File Storage for shared storage scenarios. The usage scenarios depend on the specific needs of the application.
2. Table Storage is typically used for applications that require storing large amounts of non-relational data. It's best used when you need a flexible data schema or a schemaless data store.
3. Azure SQL Database is typically used for applications that require relational database features, high availability, scalability, and security.
4. Azure SQL Elastic Pool is a shared resource model that enables higher resource utilization efficiency. It's best for a large number of databases with specific utilization patterns.
5. Azure SQL Managed Instance is a fully managed SQL Server Database Engine instance that provides near 100% compatibility with on-premises SQL Server.
6. Azure provides several types of storage redundancy including Locally redundant storage (LRS), Zone-redundant storage (ZRS), and Geo-redundant storage (GRS).
7. You can increase IOPS for a VM that hosts disk-intensive applications by choosing a disk type that provides higher IOPS, such as Premium SSDs or Ultra Disks.
8. You can implement a file share accessible from Azure and on-premises in a hybrid environment using Azure File Sync or Azure VPN Gateway.
9. The choice between Azure SQL Database, Managed Instance, and SQL Server in VM depends on factors like the level of control needed, the need for a fully managed service, and the specific features required by the application.
10. High Availability can be implemented on each of them using features like Azure SQL Database's built-in high availability, Managed Instance's instance failover groups, and SQL Server in VM's Always On availability groups.
11. CosmosDB is a globally distributed, multi-model database service. Unlike Azure SQL, it supports multiple data models such as key-value, document, column-family, and graph.
12. CosmosDB provides SDKs for several languages including .NET, Java, Python, and Node.js. It also provides a SQL API for querying the data.
13. You can scale CosmosDB by increasing the number of request units (RUs) allocated, partitioning your data, and globally distributing your data.
