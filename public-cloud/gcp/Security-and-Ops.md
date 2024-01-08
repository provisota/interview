# Security & Ops
Security and Operations in GCP involve the use of various services and practices to ensure the secure and efficient running of your applications. This includes understanding the different authentication methods, the use of IAM for access control, the hierarchy of resources and permissions, the integration of OAuth2 with IAM, the use of the Data Loss Prevention API for data classification, monitoring with Stackdriver, the hosting of Cloud Endpoints, best practices for VPC creation, and the types of keys used for encryption in managed services like GCS.

# IAM
In GCP is a suite of tools to manage access control. Service Accounts are special Google accounts that represent 
non-human users that need to authenticate and be authorized to access data in Google APIs. End-Users auth refers to the authentication of human users, typically using OAuth 2.0. Resources Hierarchy (Organization, Folders, Projects, Resources) is used to structure resources for management and access control. Policy is a binding of roles to identities, applied to a resource. A Role is a collection of permissions, and an Identity is an account that has authenticated to GCP.

# StackDriver Monitoring/Logging
Stackdriver provides Monitoring and Logging services for applications on GCP and AWS. Monitoring collects metrics, events, and metadata, and allows you to set alerts. Logging allows you to store, search, analyze, monitor, and alert on log data and events. Deployment Manager is an infrastructure deployment service that automates the creation and management of GCP resources.

# Cloud Endpoints
Cloud Endpoints is a distributed API management system providing features to develop, deploy, protect, and monitor APIs. Identity-Aware Proxy (IAP) controls access to cloud applications running on GCP. Cloud KMS (Key Management Service) is a cloud service for managing cryptographic keys for your cloud services.

# Ex-filtration Data Prevention
Ex-filtration Data Prevention refers to security measures taken to prevent sensitive data from leaving a network. Data Loss Prevention API is a service that provides programmatic access to a powerful detection engine for finding personally identifiable information and other privacy-sensitive data in text.

# Questions
1. Describe the difference between Standard Flow and API Keys for Authentication on GCP?
2. What are Policy, Roles, Identities?
3. What is the difference between custom and standard roles?
4. What types of Identities IAM supports?
5. Hierarchy of resources and permissions in IAM (org/folder/project/resource)?
6. How to secure an app with OAuth2 integrated with IAM?
7. What does the Data Loss Prevention API do?
8. How can Stackdriver monitor resources on GCP projects, AWS, On-Prem?
9. Can Cloud Endpoints be hosted on the same machine as an app?
10. Describe best practices of VPC creation, like Bastion Hosts, etc?
11. What types of keys are used for encryption in managed services (GCS) use cases?

# Answers
1. Standard Flow (OAuth 2.0) is a protocol that allows a user to grant a third-party website or application access to their protected resources, without necessarily revealing their long-term credentials or even their identity. API Keys, on the other hand, are simple encrypted strings that identify an application without any principal. They are used to access the resources of a default service account.

2. In GCP, a Policy defines who (identity) has what access (role) for which resource. A Role is a collection of permissions. An Identity is an email address that represents a user, service account, or Google group.

3. Standard roles are predefined roles that are managed by Google Cloud. Custom roles are roles that you create to tailor a set of permissions that meet the specific needs of your organization.

4. IAM supports Google Account identities (for end users), Service Account identities (for apps and virtual machines), Google group identities, and G Suite domain identities.

5. In IAM, the hierarchy of resources and permissions goes from the Organization level to the Folder level, then to the Project level, and finally to the Resource level. Permissions are inherited down the hierarchy.

6. To secure an app with OAuth2 integrated with IAM, you can use the OAuth 2.0 protocol for authentication and authorization. Google Cloud uses OAuth 2.0 for API authentication and authorization.

7. The Data Loss Prevention API provides methods for detection of privacy-sensitive fragments in text, images, and Google Cloud Storage.

8. Stackdriver can monitor resources on GCP projects, AWS, and on-premises through the installation of monitoring agents on the VM instances.

9. Cloud Endpoints can be hosted on the same machine as an app if the app is hosted on a Google Cloud VM instance.

10. Best practices for VPC creation include the use of multiple subnets for isolation, the use of firewall rules to control traffic, and the use of Bastion Hosts for secure administrative access.

11. In managed services like GCS, Google-managed keys, customer-supplied encryption keys, and customer-managed encryption keys are used for encryption.