# Security & Ops

## IAM
IAM, or Identity and Access Management, is a framework of business processes, policies, and technologies that facilitates the management of electronic or digital identities in Azure. With IAM, you can control who has access to what resources in your Azure environment.

## Service Accounts
Service Accounts in Azure are special accounts that are used by services and applications running on a VM to interact with other Azure services.

## End-Users auth
End-Users authentication in Azure can be managed using Azure Active Directory, which supports a wide range of identity providers and offers identity protection, access reviews, and more.

## Resources Hierarchy
In Azure, resources are organized hierarchically into management groups, subscriptions, resource groups, and resources. This hierarchy allows you to manage access, policies, and compliance across multiple Azure subscriptions.

## Policy/Role/Identity
Azure Policy is a service in Azure that you use to create, assign, and manage policies. These policies enforce different rules and effects over your resources, so those resources stay compliant with your corporate standards and service level agreements.

## Azure Key Vault
Azure Key Vault is a service that provides a secure store for secrets, such as keys, passwords, certificates, or other secrets. It can be used to manage and control access to these secrets.

## ARM
Azure Resource Manager (ARM) is the deployment and management service for Azure. It provides a management layer that enables you to create, update, and delete resources in your Azure subscription.

## Terraform
Terraform is an open-source infrastructure as code software tool that provides a consistent CLI workflow to manage hundreds of cloud services. Terraform codifies APIs into declarative configuration files.

## Application Insights
Application Insights is an extensible Application Performance Management (APM) service for developers and DevOps professionals. It can be used to monitor your live applications, detect performance anomalies, and diagnose issues with your applications.

## Azure Monitor
Azure Monitor maximizes the availability and performance of your applications by delivering a comprehensive solution for collecting, analyzing, and acting on telemetry from your cloud and on-premises environments.

## Azure Security Center
Azure Security Center is a unified infrastructure security management system that strengthens the security posture of your data centers, and provides advanced threat protection across your hybrid workloads in the cloud.

## Secure Devops Toolkit
The Secure DevOps Kit for Azure (AzSK) is a collection of scripts, tools, extensions, automations, etc. that caters to the end-to-end Azure subscription and resource security needs for dev ops teams using extensive automation and smoothly integrating security into native dev ops workflows.

## Questions
1. What is the recommended way to store secrets in Azure?
2. How to assess security level of a given cloud environment?
3. What are the options for automatic env deployment to Azure?
4. How to speed up automatic deployment?
5. What are the features of Application Insights?
6. What is Azure Monitor and what are the main features?

## Answers
1. The recommended way to store secrets in Azure is to use Azure Key Vault.
2. You can assess the security level of a given cloud environment using Azure Security Center and Azure Policy.
3. Options for automatic environment deployment to Azure include using Azure Resource Manager (ARM) templates, Azure DevOps, and third-party tools like Terraform.
4. You can speed up automatic deployment by using parallel deployments in ARM templates, using incremental mode in ARM templates, and by optimizing your pipeline in Azure DevOps.
5. Application Insights provides features like application performance monitoring, log analytics, user behavior analytics, and integration with popular DevOps tools.
6. Azure Monitor provides features like application and network performance monitoring, log analytics, and integration with popular DevOps tools. It also provides advanced analytics and visualization capabilities through Azure Log Analytics and Azure Dashboards.