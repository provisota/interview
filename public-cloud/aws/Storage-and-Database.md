# Storage and Database
1. **Object Storage**: Amazon S3 (Simple Storage Service) is an object storage service that offers industry-leading scalability, data availability, security, and performance. S3 offers different storage classes for different use cases (like S3 Standard, S3 Intelligent-Tiering, S3 Standard-IA, and S3 One Zone-IA). Lifecycle rules can be used to automatically move objects between storage classes or expire objects that are no longer needed. Access to static content can be controlled using Access Control Lists (ACLs) or bucket policies. Token Access (Pre-signed URLs) can be used to grant temporary access to private objects. For highload optimizations, you can use features like Transfer Acceleration or multipart uploads.

2. **Migrations**: AWS provides several services for data migration. Database Migration Service (DMS) can be used to migrate databases to AWS easily and securely. Snowball is a petabyte-scale data transport solution that uses secure appliances to transfer large amounts of data into and out of the AWS Cloud. Storage Gateway is a hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage.

3. **Block Storage**: Amazon EBS (Elastic Block Store) provides block level storage volumes for use with EC2 instances. EBS volumes are network attached, and persist independently from the life of an instance. Amazon EFS (Elastic File System) provides a simple, scalable, fully managed elastic NFS file system for use with AWS Cloud services and on-premises resources. RAID (Redundant Array of Independent Disks) can be used to increase the I/O performance of EBS volumes.

4. **Managed DBs**: AWS provides several managed database services. Amazon RDS (Relational Database Service) makes it easy to set up, operate, and scale a relational database in the cloud. Amazon Aurora is a MySQL and PostgreSQL-compatible relational database built for the cloud. Amazon Redshift is a fast, scalable data warehouse that makes it simple and cost-effective to analyze all your data across your data warehouse and data lake. Amazon DynamoDB is a key-value and document database that delivers single-digit millisecond performance at any scale. Amazon DAX (DynamoDB Accelerator) is a fully managed, highly available, in-memory cache for DynamoDB. Amazon Neptune is a fast, reliable, fully-managed graph database service. Amazon ElastiCache offers fully managed Redis and Memcached. Amazon Elasticsearch Service is a fully managed service that makes it easy to deploy, secure, and operate Elasticsearch at scale. Amazon DocumentDB (with MongoDB compatibility) is a fast, scalable, highly available, and fully managed document database service.
# Questions
1. Describe Data Consistent Model for AWS S3?
2. What storage types present in S3, what has the highest SLAs and HA?
3. How to implement static content hosting with S3(what is CORS)?
4. What types of EBS exist, how to back up and restore encrypted EBS in another region?
5. Bucket policies and Encryption types of S3 for transit and at rest, how to specify encryption type ?
6. How to transfer big amounts of data from DC to Cloud?
7. What is the difference between instance store and EBS?
8. Describe LSI, GSI, how to design RCU/WCU?
9. Types of replicas supported for RDS, differences between them?
10. Describe supported Cache engines of ElasticCache and its use cases?
11. Difference between Lazy loading and Write Through Cache strategies
# Answers
1. AWS S3 provides strong read-after-write consistency for PUTS of new objects and eventual consistency for overwrite PUTS and DELETES. This means that if you write a new object to S3, you can immediately read the object. However, if you overwrite or delete an existing object, it might take some time for the change to propagate.

2. S3 offers several storage classes: S3 Standard for general-purpose storage of frequently accessed data; S3 Intelligent-Tiering for data with unknown or changing access patterns; S3 Standard-IA and One Zone-IA for long-lived, but less frequently accessed data; S3 Glacier and S3 Glacier Deep Archive for long-term archive and digital preservation. S3 Standard offers the highest level of durability and availability.

3. To host static content with S3, you can create an S3 bucket, enable static website hosting in the bucket properties, and upload your content. CORS (Cross-Origin Resource Sharing) is a mechanism that allows many resources (e.g., fonts, JavaScript, etc.) on a web page to be requested from another domain outside the domain from which the resource originated.

4. EBS provides several volume types: General Purpose SSD (gp2), Provisioned IOPS SSD (io1), Throughput Optimized HDD (st1), and Cold HDD (sc1). To back up an EBS volume, you can create a snapshot of the volume. To restore, you can create a new volume from the snapshot in another region.

5. S3 bucket policies are used to grant permissions to S3 buckets. You can specify the encryption type for an S3 bucket by enabling default encryption in the bucket properties. S3 supports several encryption options for data at rest, including S3 managed keys (SSE-S3), AWS Key Management Service (SSE-KMS), and server-side encryption with customer-provided keys (SSE-C). For data in transit, S3 supports SSL/TLS.

6. To transfer large amounts of data from a data center to the cloud, you can use AWS Direct Connect for a dedicated network connection, AWS Snowball for a physical data transport solution, or AWS DataSync for online data transfer.

7. An instance store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer. EBS is a persistent storage that exists independently from your instance and can be attached to any EC2 instance in the same Availability Zone.

8. In DynamoDB, a Local Secondary Index (LSI) is an index that has the same partition key as the table, but a different sort key. A Global Secondary Index (GSI) is an index with a partition key and sort key that can be different from those on the table. Read Capacity Units (RCU) and Write Capacity Units (WCU) are the units for measuring read and write capacity.

9. RDS supports several types of replicas: Read Replicas for offloading read traffic from the primary database instance, and Multi-AZ deployments for disaster recovery and failover support.

10. ElastiCache supports two open-source in-memory caching engines: Memcached and Redis. Use cases include improving the performance of web applications by retrieving information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.

11. Lazy Loading is a design pattern which delays the loading or initialization of resources until they are needed. Write Through Cache is a caching strategy where data is simultaneously written into the cache and the backing store. The main difference between the two is that lazy loading fetches data only when necessary, while write through cache updates the cache and the data source every time there's a write operation.