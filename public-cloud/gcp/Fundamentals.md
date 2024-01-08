# GCP Fundamentals
1. Key components in GCP include:
   - IAM (Identity and Access Management): Manages access control by defining who (identity) has what access (role) for which resource.
   - Machine Images: A compute resource that contains all the data necessary to create a virtual machine (VM) instance.
   - Storages: GCP provides different storage services like Cloud Storage (object storage), Persistent Disk (block storage), and Cloud Filestore (file storage) to store and retrieve data.
   - Queues: Cloud Tasks and Pub/Sub are used for asynchronous workloads and messaging respectively.

2. Compute instance types in GCP are categorized based on their intended use-case. They include:
   - General-purpose: Balanced performance for a variety of workloads.
   - Memory-optimized: Ideal for memory-intensive workloads.
   - Compute-optimized: Ideal for compute-intensive workloads.
   - GPU instances: Ideal for ML, scientific computations, and 3D visualizations.
     Scaling of VM instances in GCP can be achieved using managed instance groups (MIGs). MIGs maintain high availability of your applications by proactively keeping your VM instances available, that is, in the RUNNING state. MIGs can automatically increase or decrease the number of VM instances (auto scaling) based on increases or decreases in load.

3. Availability Zones in GCP are called zones. They are physically isolated locations within a region. Regions are independent geographic areas that consist of zones. Zones are deployment areas for GCP resources within regions. Zones should be considered a single failure domain within a region. By deploying applications across multiple zones and regions, you can ensure high availability and disaster recovery.

# Questions
1. What are GCP key components and what goal they serve?
2. What is VPC? (ask few questions on key components)
3. Which compute instance types do you know and what for those are optimized?
4. How to scale VM instances?
5. Availability zones and regions

# Answers
1. GCP key components and their goals: IAM (Identity and Access Management) manages access control, Machine Images are compute resources that contain all the data necessary to create a virtual machine (VM) instance, Storages like Cloud Storage for object storage, and Queues like Cloud Tasks for asynchronous workloads.
2. VPC (Virtual Private Cloud) is a global resource that consists of a list of regional virtual subnetworks (subnets) in data centers, all connected by a global wide area network.
3. GCP provides various compute instance types optimized for different needs: General-purpose for balanced performance, Memory-optimized for memory-intensive workloads, Compute-optimized for compute-intensive workloads, and GPU instances for ML, scientific computations, and 3D visualizations.
4. Scaling VM instances in GCP can be achieved using managed instance groups (MIGs). MIGs maintain high availability of your applications by proactively keeping your VM instances available.
5. Availability Zones in GCP are called zones. They are physically isolated locations within a region. Regions are independent geographic areas that consist of zones. Zones are deployment areas for GCP resources within regions.