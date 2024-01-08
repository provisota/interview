# Infrastructure as a Service (IaaS)
Infrastructure as Code (IaC) is a method of managing and provisioning computing infrastructure with machine-readable definition files, rather than physical hardware configuration or interactive configuration tools. It's a key practice in the DevOps movement and is used in conjunction with continuous delivery.

Terraform, AWS CloudFormation, Azure ARM, and GCP Cloud Deployment Manager are all tools that support IaC. They allow you to define and provide data center infrastructure using a declarative configuration language and deploy it using a command line interface.

- **Terraform**: An open-source IaC software tool created by HashiCorp. It enables users to define and provide data center infrastructure using a declarative configuration language. Terraform supports a multitude of providers such as AWS, GCP, Azure, Alibaba, and many more.

- **AWS CloudFormation**: A service that helps you model and set up Amazon Web Services resources so you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and AWS CloudFormation takes care of provisioning and configuring those resources for you.

- **Azure ARM (Azure Resource Manager)**: Azure Resource Manager is the deployment and management service for Azure. It provides a management layer that enables you to create, update, and delete resources in your Azure account. You use management features, like access control, locks, and tags, to secure and organize your resources after deployment.

- **GCP Cloud Deployment Manager**: Google Cloud Deployment Manager allows you to specify all the resources needed for your application in a declarative format using yaml. You can also use Python or Jinja2 templates to parameterize the configuration and allow reuse of common deployment paradigms such as a load balanced, auto-scaled instance group.
# Questions
1. What is IaC, its pros and cons?
2. Immutable vs  mutable infrastructure.
3. Declarative vs imperative approach.
4. GitOps principles
5. Can you use Terraform with different cloud providers?
6. How to store Terraform code in the codebase (what to do with state files)?
7. Terraform vs AWS Cloud Formation vs Azure AMR Templates vs GCP Cloud Deployment Manager
# Answers
1. Infrastructure as Code (IaC) is a method of managing and provisioning computing infrastructure with machine-readable definition files, rather than physical hardware configuration or interactive configuration tools. The pros of IaC include speed and efficiency, consistency and repeatability, scalability, and reduced risk. The cons include the learning curve, the need for a culture of automation, and the potential for configuration drift if not properly managed.

2. Immutable infrastructure is an approach where servers are never modified after they're deployed. If a server needs to be updated, fixed, or modified in any way, new servers are built from a common image with the necessary changes, and the old servers are discarded. Mutable infrastructure, on the other hand, is an approach where changes are applied to existing servers.

3. Declarative approach describes the desired state of the system, and the tooling determines how to achieve that state. In contrast, the imperative approach specifies the exact commands to change the system from its current state to the desired state.

4. GitOps is a way of implementing Continuous Deployment for cloud native applications. It uses Git as a single source of truth for declarative infrastructure and applications. With Git at the center of your delivery pipelines, developers can make pull requests to accelerate and simplify application deployments and operations tasks to Kubernetes.

5. Yes, Terraform can be used with different cloud providers. It supports a multitude of providers such as AWS, GCP, Azure, Alibaba, and many more.

6. Terraform code can be stored in the codebase just like any other code. However, Terraform state files (which are generated when Terraform applies your configurations) should not be stored in the codebase. They can contain sensitive data and they can cause conflicts if multiple people are running Terraform at the same time. Instead, state files should be stored in a secure, shared location, and Terraform supports storing state remotely in places like AWS S3, Google Cloud Storage, or Terraform Cloud.

7. Terraform, AWS CloudFormation, Azure ARM Templates, and GCP Cloud Deployment Manager are all tools for managing infrastructure as code. They have different syntax and support different sets of providers. Terraform is multi-cloud and provider-agnostic, whereas CloudFormation, ARM Templates, and Cloud Deployment Manager are designed to work with AWS, Azure, and GCP respectively.