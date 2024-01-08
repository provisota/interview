# Security and Ops
1. **Organization/Account, IAM, SAML, STS, types of access, concept of roles, policies, service accounts, MFA, permission types**: AWS Organizations allows you to centrally manage and govern your environment as you grow and scale your AWS resources. IAM (Identity and Access Management) is a web service that helps you securely control access to AWS resources. SAML (Security Assertion Markup Language) is an open standard for exchanging authentication and authorization data between parties. STS (Security Token Service) is a web service that enables you to request temporary, limited-privilege credentials for IAM users or for users that you authenticate (federated users). AWS supports several types of access, including programmatic access, AWS Management Console access, and SSH access. Roles in AWS allow you to delegate access to users or services that normally don't have access to your organization's AWS resources. IAM policies define permissions for an action regardless of the method that you use to perform the operation. Service accounts are used by services (not users) to interact with other services. MFA (Multi-Factor Authentication) adds an extra layer of protection on top of your user name and password.

2. **Shared security responsibility Model**: In AWS, security is shared between AWS and the customer. AWS is responsible for protecting the infrastructure that runs all of the services offered in the AWS Cloud. This is often referred to as security “of” the cloud. The customer responsibility is determined by the AWS service that is being used. This is often referred to as security “in” the cloud.

3. **CloudWatch, CloudTrail, X-Ray**: Amazon CloudWatch is a monitoring and observability service built for DevOps engineers, developers, site reliability engineers (SREs), and IT managers. AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture.

4. **CloudHSM, KMS, data encryption at rest and in transit, System manager Parameter Store, Cognito**: AWS CloudHSM is a cloud-based hardware security module (HSM) that enables you to easily generate and use your own encryption keys on the AWS Cloud. AWS Key Management Service (KMS) makes it easy for you to create and manage cryptographic keys and control their use across a wide range of AWS services. AWS provides several methods for encrypting data at rest and in transit. AWS Systems Manager Parameter Store provides secure, hierarchical storage for configuration data management and secrets management. Amazon Cognito lets you add user sign-up, sign-in, and access control to your web and mobile apps quickly and easily.

5. **Opswork, CloudFormation**: AWS OpsWorks is a configuration management service that provides managed instances of Chef and Puppet. AWS CloudFormation provides a common language for you to describe and provision all the infrastructure resources in your cloud environment.
# Questions
1. What are best practices to apply role access to machines and on App level?
2. CodeDeploy difference in In-Place and Blue/Green deployments?
3. How will you store CREDs on AWS?
4. What types of encryption are supported to S3, how they are configured and used?
5. Describe difference between CloudHSM and KMS?
6. STS usage and flows?
# Answers
1. Best practices to apply role access to machines and at the App level include:
    - Principle of Least Privilege: Grant only the permissions required to perform a task.
    - Use IAM roles: Assign IAM roles to EC2 instances instead of using access keys.
    - Use IAM roles for applications: Applications running on an EC2 instance should use the instance's role to get temporary credentials.
    - Regularly rotate credentials: Regularly rotate and remove unused credentials.
    - Audit: Regularly audit your IAM settings and permissions with AWS CloudTrail.

2. In AWS CodeDeploy, In-Place deployments replace the current application on an instance while Blue/Green deployments provision new instances, deploy the application to the new instances, and then switch traffic to the new instances. Blue/Green deployments minimize downtime and risk by making the switch instant and by allowing easy rollback if issues are detected.

3. On AWS, credentials should be stored securely using services like AWS Secrets Manager or Systems Manager Parameter Store. These services encrypt the credentials at rest and provide controlled access through IAM policies.

4. Amazon S3 supports several types of encryption for data at rest, including S3 managed keys (SSE-S3), AWS Key Management Service (SSE-KMS), and customer provided keys (SSE-C). For data in transit, S3 supports SSL/TLS.

5. AWS CloudHSM and KMS are both used for cryptographic key storage, but they serve different needs. CloudHSM provides a dedicated hardware security module (HSM) instance for high-performance cryptographic operations and key storage, and you manage the cryptographic keys. KMS is a managed service that makes it easier for you to create and control the cryptographic keys used for data encryption, and it's integrated with other AWS services.

6. AWS Security Token Service (STS) is a service that provides temporary security credentials that you can use to access AWS services that you might not normally have access to. These temporary credentials consist of an access key ID, a secret access key, and a security token. Typical STS workflows might include federation (single sign-on), identity delegation (a mobile app that assumes an IAM role to get temporary credentials for accessing AWS resources), or cross-account access (you own multiple AWS accounts and need to access resources in one account from another).