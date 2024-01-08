# AWS Fundamentals
1. Key AWS Components:
    - **EC2 (Elastic Compute Cloud)**: Provides resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers.
    - **AMI (Amazon Machine Image)**: A template that contains a software configuration (for example, an operating system, an application server, and applications). From an AMI, you launch instances, which are copies of the AMI running as virtual servers in the cloud.
    - **IAM (Identity and Access Management)**: Enables you to manage access to AWS services and resources securely. Using IAM, you can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources.
    - **Storages**: AWS provides a variety of storage services such as S3 (Simple Storage Service) for object storage, EBS (Elastic Block Store) for persistent block storage for use with EC2 instances, and more.
    - **Queues**: AWS provides queuing services through SQS (Simple Queue Service), a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.

2. EC2 Instance Types and Scaling:
    - **EC2 Instance Types**: EC2 provides a variety of instance types optimized to fit different use cases, based on memory, compute capacity, and storage capacity.
    - **Scaling**: AWS provides Auto Scaling to automatically adjust the number of EC2 instances in response to traffic patterns. This helps ensure that you have the right number of EC2 instances available to handle the load for your application.

3. Availability Zones and Regions:
    - **Availability Zones**: Each region is fully isolated from the other regions and is made up of one or more isolated locations known as Availability Zones. Each Availability Zone is isolated, but the Availability Zones in a region are connected through low-latency links.
    - **Regions**: AWS resources are hosted in multiple locations worldwide. These locations are composed of regions and Availability Zones. Each region is a separate geographic area.
# Questions
1. What are AWS key components and what goal they serve?
2. What is VPC? (ask few questions on key components)
3. What instance types do you know and what for those are optimized?
4. How to scale EC2 instances?
5. Availability zones and regions
# Answers
1. AWS Key Components:
    - **EC2 (Elastic Compute Cloud)**: Provides resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers.
    - **AMI (Amazon Machine Image)**: A template that contains a software configuration (for example, an operating system, an application server, and applications). From an AMI, you launch instances, which are copies of the AMI running as virtual servers in the cloud.
    - **IAM (Identity and Access Management)**: Enables you to manage access to AWS services and resources securely. Using IAM, you can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources.
    - **Storages**: AWS provides a variety of storage services such as S3 (Simple Storage Service) for object storage, EBS (Elastic Block Store) for persistent block storage for use with EC2 instances, and more.
    - **Queues**: AWS provides queuing services through SQS (Simple Queue Service), a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.

2. VPC (Virtual Private Cloud) is a virtual network dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS Cloud. You can launch your AWS resources, such as Amazon EC2 instances, into your VPC. You can configure your VPC by modifying its IP address range, create subnets, and configure route tables, network gateways, and security settings.

3. AWS provides a variety of EC2 instance types optimized for different use cases:
    - **General Purpose**: Balanced compute, memory, and networking resources (e.g., M5 instances).
    - **Compute Optimized**: Ideal for compute-bound applications that benefit from high-performance processors (e.g., C5 instances).
    - **Memory Optimized**: Designed to deliver fast performance for workloads that process large data sets in memory (e.g., R5 instances).
    - **Storage Optimized**: Designed for workloads that require high, sequential read and write access to very large data sets on local storage (e.g., H1 instances).

4. To scale EC2 instances, you can use AWS Auto Scaling. It allows you to automatically adjust the number of EC2 instances in response to traffic patterns. You can set scaling policies based on criteria such as CPU utilization or network traffic.

5. Availability Zones and Regions: AWS resources are hosted in multiple locations worldwide. These locations are composed of regions and Availability Zones. Each region is a separate geographic area, and each region has multiple, isolated locations known as Availability Zones. This structure allows you to design and operate applications and databases that are highly available, fault-tolerant, and scalable.