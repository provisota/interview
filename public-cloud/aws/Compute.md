# Compute
1. **EC2 (Elastic Compute Cloud)**: EC2 is a web service that provides resizable compute capacity in the cloud. It is designed to make web-scale computing easier for developers. EC2 offers a variety of machine types optimized for different use cases, from general purpose to compute optimized, memory optimized, and more. Spot instances are an EC2 feature that allows you to take advantage of unused EC2 capacity in the AWS cloud. Spot instances are available at up to a 90% discount compared to On-Demand prices. You can use Spot Instances for various stateless, fault-tolerant, or flexible applications such as big data, containerized workloads, CI/CD, web servers, high-performance computing (HPC), and other test & development workloads. Cloud-init is a package that contains utilities for early initialization of cloud instances. It is installed in the EC2 Amazon Machine Images (AMIs) and it allows you to configure the instance using a script at launch time.

   **Elastic Beanstalk**: AWS Elastic Beanstalk is an easy-to-use service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and IIS. You can simply upload your code and Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, auto-scaling to application health monitoring.

2. **EKS (Elastic Kubernetes Service)**: EKS is a managed service that makes it easy for you to run Kubernetes on AWS without needing to install and operate your own Kubernetes control plane. It provides a scalable and highly-available control plane that runs across multiple AWS availability zones.

   **ECS (Elastic Container Service)**: ECS is a highly scalable, high-performance container orchestration service that supports Docker containers and allows you to easily run and scale containerized applications on AWS. ECS eliminates the need for you to install and operate your own container orchestration software, manage and scale a cluster of virtual machines, or schedule containers on those virtual machines.

   **ECR (Elastic Container Registry)**: ECR is a fully-managed Docker container registry that makes it easy for developers to store, manage, and deploy Docker container images. ECR is integrated with Amazon ECS and Amazon EKS, simplifying your development to production workflow.
# Questions
1. What is AMI, how to use it?
2. How to add custom logic, packets installation on VM start?
3. How to configure scale up/down EC2 machines based on load/demand, what are the best practices, proactive scaling, etc?
4. What types of EC2 instances do you know (difference between on-demand/reserved/spot)?
5. EKS security and billing?
6. When to use EKS, ECS, ECR?
7. ElasticBeanStalk deployment types (all-at-once/rolling/with batch/immutable) use cases differences?
# Answers
1. An Amazon Machine Image (AMI) is a template that contains a software configuration (for example, an operating system, an application server, and applications). From an AMI, you launch instances, which are copies of the AMI running as virtual servers in the cloud. You can use pre-configured AMIs provided by AWS, or create your own AMIs and use them to launch instances.

2. To add custom logic or install packages on an EC2 instance at startup, you can use user data scripts. User data scripts are run as the root user, and they can be used to perform common automated configuration tasks and even run scripts after the instance starts.

3. To configure auto-scaling of EC2 instances based on load or demand, you can use AWS Auto Scaling. You can create scaling policies based on criteria such as CPU utilization or network traffic. AWS also provides predictive scaling as a feature of AWS Auto Scaling, which uses machine learning to schedule the right number of instances ahead of predicted demand.

4. EC2 instances come in several types, which are optimized for different use cases:
    - On-Demand Instances: Let you pay for compute capacity by the hour with no long-term commitments.
    - Reserved Instances: Provide you with a significant discount (up to 75%) compared to On-Demand instance pricing.
    - Spot Instances: Allow you to bid on spare Amazon EC2 computing capacity for up to 90% off the On-Demand price.

5. EKS (Elastic Kubernetes Service) security involves using IAM for access control, running your EKS clusters inside a VPC, and using security groups to control network access to your instances. For billing, you pay $0.10 per hour for each EKS cluster that you create.

6. You would use EKS when you want to run Kubernetes without managing the underlying infrastructure, ECS (Elastic Container Service) when you want a simpler, more integrated AWS experience for running containers, and ECR (Elastic Container Registry) when you need a Docker container registry to store your container images.

7. Elastic Beanstalk supports several deployment types:
    - All at once: Deploys the new version to all instances simultaneously. All instances are out of service while the deployment takes place.
    - Rolling: Deploys the new version in batches. Each batch of instances is taken out of service while the deployment takes place.
    - Rolling with additional batch: Similar to Rolling, but launches a new batch of instances to ensure full capacity during the deployment process.
    - Immutable: Launches a full set of new instances in a new Auto Scaling group. If the deployment is successful, Elastic Beanstalk shifts the load balancer to the new instances. If not, it simply terminates the new instances.