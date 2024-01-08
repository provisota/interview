# Azure fundamentals

## Resource Group
A Resource Group in Azure is a logical container for resources deployed within an Azure subscription. This group usually contains resources that are meant to have the same lifecycle and are related to the same application.

## IAM
IAM, or Identity and Access Management, is a framework of business processes, policies, and technologies that facilitates the management of electronic or digital identities in Azure. With IAM, you can control who has access to what resources in your Azure environment.

## ARM
Azure Resource Manager (ARM) is the deployment and management service for Azure. It provides a management layer that enables you to create, update, and delete resources in your Azure subscription.

## SKU
SKU, or Stock Keeping Unit, in Azure refers to the characteristics of a resource such as its tier, performance level, or capacity. These characteristics are used to track inventory or provision resources.

## Storages & Queues
Azure provides various storage services like Blob Storage, File Storage, Queue Storage, and Table Storage. Azure Queue Storage is a service for storing large numbers of messages that can be accessed from anywhere in the world.

## VM types
Azure provides a variety of virtual machine (VM) types tailored to different needs and workloads. These include general-purpose VMs, compute-optimized VMs, memory-optimized VMs, storage-optimized VMs, and GPU VMs.

## Scaling
Scaling in Azure refers to the ability to increase or decrease the amount of resources allocated to your application based on its demand. This can be done either manually, or automatically using Azure's autoscaling feature.

## Availability
Availability in Azure refers to the time that a service is up and running. It is usually measured as a percentage, with a higher percentage indicating more reliable service.

## Startup scripts
Startup scripts in Azure are scripts that you can configure to run during a service's startup phase. You can use these scripts to install software, configure settings, or perform other tasks.

## Regions
A region in Azure is a set of datacenters deployed within a latency-defined perimeter and connected through a dedicated regional low-latency network.

## Paired Regions
Paired regions in Azure are a pair of regions that are geographically located within the same broader geographical area for disaster recovery purposes.

## Availability Zones
Availability Zones in Azure are physically separate locations within an Azure region. Each Availability Zone is made up of one or more datacenters equipped with independent power, cooling, and networking.

## Questions
1. What is Resource Group? How it is related to Regions?
2. What is ARM Templates?
3. What storages are commonly used?
4. What queues are commonly used?
5. What is a region? How is it different from a datacenter?
6. What is the concept of paired regions? How paired regions are different from any two regions?
7. What is the availability zone?
8. How to create a VM with pre-installed software?
9. How to run startup scripts on a VM?
10. How to scale an application deployed on VMs?

## Answers
1. A Resource Group in Azure is a logical container for resources deployed within an Azure subscription. It is related to regions as each resource within a resource group can be located in different regions.
2. ARM Templates are JSON files that define the resources you need to deploy for your solution. It provides a declarative way to define deployment.
3. Commonly used storages in Azure include Blob Storage for unstructured data, File Storage for file shares, Table Storage for NoSQL data, and Queue Storage for messaging.
4. Azure Queue Storage is commonly used for storing large numbers of messages that can be accessed from anywhere in the world.
5. A region in Azure is a set of datacenters deployed within a latency-defined perimeter and connected through a dedicated regional low-latency network. A datacenter is a part of a region.
6. Paired regions in Azure are a pair of regions that are geographically located within the same broader geographical area for disaster recovery purposes. They are different from any two regions as they have a specific relationship for replication and failover.
7. Availability Zones in Azure are physically separate locations within an Azure region. Each Availability Zone is made up of one or more datacenters equipped with independent power, cooling, and networking.
8. To create a VM with pre-installed software, you can use Azure Marketplace images or use custom images that you create.
9. To run startup scripts on a VM, you can use the Custom Script Extension in Azure.
10. To scale an application deployed on VMs, you can use Azure's autoscaling feature which allows you to automatically increase or decrease the number of VM instances based on demand or a schedule.