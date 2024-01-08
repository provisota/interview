# Storages & Databases
Google Cloud Storage (GCS) offers different storage classes for different use cases: Standard for frequently accessed data, Nearline for infrequently accessed data, Coldline for cold storage, and Archive for long-term archiving. GCS supports server-side encryption with either Google-managed, customer-supplied, or customer-managed encryption keys.

Temporary access to a GCS bucket can be provided using signed URLs or IAM conditions.

Google Cloud SQL is a fully managed relational database service that provides high availability (HA) through automatic failover to replicas in different zones.

Google Cloud Spanner is a globally distributed, horizontally scalable, strongly consistent relational database service. It provides capabilities such as global transactions, SQL querying, and automatic multi-site replication and failover.

# Object Storage: GCS
Google Cloud Storage (GCS) is an object storage service for storing and accessing data. It offers different storage classes (Standard, Nearline, Coldline, and Archive) depending on the frequency of access. Retention policies can be set to automatically delete objects after a specified period. GCS supports server-side encryption and customer-supplied encryption keys. The Storage Transfer Service allows you to move data into, out of, and within GCS.

# Block Storage
Google Cloud Platform offers two types of block storage: standard hard disk drives (HDD) and solid-state drives (SSD). Standard HDDs are cost-effective and suitable for applications with low IOPS requirements. SSDs are more expensive but provide higher performance and are suitable for applications with high IOPS requirements. Google Filestore is a managed file storage service for applications that require a filesystem interface and a shared filesystem for data.

# Managed DBs
Google Cloud Platform offers several managed database services:
- Cloud SQL: Fully managed relational database service for MySQL, PostgreSQL, and SQL Server.
- Cloud Spanner: Globally distributed, horizontally scalable, relational database service that also provides strong consistency across regions and high availability.
- Bigtable: NoSQL big data database service that is suitable for web, mobile, and IoT applications and for real-time analytics.
- Firestore: NoSQL document database for mobile, web, and server development.
- Memorystore: Fully managed in-memory data store service for Redis and Memcached.
- Data Transfer: Service for migrating databases to Google Cloud. It supports offline and online migrations.

# Questions
1. What are the differences in GCS storage classes?
2. How to set up encryption in GCS? What encryption types are available?
3. How to provide temporary access to a GCS bucket?
4. What are typical use cases for each managed database service?
5. What do you need to do to set up HA in a Cloud SQL database?
6. Which of the managed DB services provide strong consistency?
7. What capabilities does Cloud Spanner provide?

# Answers
1. GCS storage classes include Standard for frequently accessed data, Nearline for infrequently accessed data, Coldline for cold storage, and Archive for long-term archiving.
2. Encryption in GCS can be set up using server-side encryption with either Google-managed, customer-supplied, or customer-managed encryption keys.
3. Temporary access to a GCS bucket can be provided using signed URLs or IAM conditions.
4. Typical use cases for managed database services include transactional workloads for Cloud SQL, globally distributed applications for Cloud Spanner, and large-scale analytical workloads for BigQuery.
5. To set up HA in a Cloud SQL database, you need to configure it to have replicas in different zones and enable automatic failover.
6. Cloud Spanner is a managed DB service that provides strong consistency.
7. Cloud Spanner provides capabilities such as global transactions, SQL querying, and automatic multi-site replication and failover.