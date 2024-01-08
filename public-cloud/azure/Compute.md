# Compute

## VMs
Virtual Machines (VMs) in Azure are software emulations of physical computers. They provide the functionality of a physical computer, running an operating system and applications, and provide the flexibility of virtualization without the costs of physically maintaining the hardware.

## Fault domains
A fault domain in Azure is a logical group of hardware in a data center that shares a common power source and network switch. It is designed to ensure that during a hardware failure only a small subset of VM instances are affected and your application stays up.

## Update domains
Update domains in Azure are logical groups of VMs that Azure can update at the same time. They are used to ensure that not all VMs are updated at the same time during planned maintenance.

## PaaS
Platform as a Service (PaaS) in Azure is a complete development and deployment environment in the cloud. It provides resources such as servers, storage, and networking, as well as services such as team collaboration, application development and testing, and application lifecycle management.

## Azure App Service
Azure App Service is a fully managed platform for building, deploying, and scaling web apps. You can host web apps, mobile app back ends, RESTful APIs, or automated business processes.

## Containers
Containers in Azure provide a lightweight, isolated environment for running applications. They are a solution to the problem of how to get software to run reliably when moved from one computing environment to another.

## AKS
Azure Kubernetes Service (AKS) is a managed container orchestration service provided by Azure. It simplifies the deployment, scaling, and operations of containerized applications using Kubernetes, an open-source container orchestration platform.

## ACI
Azure Container Instances (ACI) is a service that allows you to run containers directly on Azure, without the need to manage any underlying infrastructure.

## Docker based App Service
Docker based App Service is a feature of Azure App Service that allows you to deploy and run containerized applications. You can package your application into a Docker container, upload it to a registry, and then deploy the container to App Service.

## Service Fabric
Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.

## Questions
1. What are the concepts of fault domain and update domain?
2. How to create a VM that will have the SLA of at least 99.9 guaranteed by Azure?
3. What are the options when deploying an application to Azure App Service?
4. How to configure security for App Service?
5. How to scale App Service?
6. How to implement zero-downtime deployments with Azure App Service?
7. Is it possible to implement A/B testing using Azure App Service?
8. How to connect App Service to a VNET?
9. What are the options to monitor App Service?
10. What are the options to deploy a container to Azure? Which are pros and cons for each of them? Are all the options supported for Windows Containers?

## Answers
1. Fault domains are logical groups of hardware that share a common power source and network switch, designed to limit the impact of hardware failures. Update domains are logical groups of VMs that Azure can update at the same time during planned maintenance.
2. To create a VM with an SLA of at least 99.9%, you need to use at least two VMs in an Availability Set or use VMs with Premium Storage.
3. You can deploy an application to Azure App Service using Git, FTP, local Git, GitHub, Bitbucket, Docker Hub, or Azure Container Registry.
4. You can configure security for App Service using SSL bindings, IP restrictions, client certificate authentication, and Azure Active Directory.
5. You can scale App Service manually, automatically based on a schedule, or automatically based on metrics.
6. You can implement zero-downtime deployments with Azure App Service using deployment slots and staged deployments.
7. Yes, you can implement A/B testing using Azure App Service with Traffic Routing feature.
8. You can connect App Service to a VNET using VNet Integration.
9. You can monitor App Service using Azure Monitor, Log Stream, and App Service diagnostics.
10. You can deploy a container to Azure using Azure Kubernetes Service (AKS), Azure Container Instances (ACI), or Docker-based App Service. All options support Windows Containers. AKS is best for complex applications with many components, ACI is best for simple applications or temporary workloads, and Docker-based App Service is best for web applications.