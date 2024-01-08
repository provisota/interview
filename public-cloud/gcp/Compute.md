# GCP Compute
Google Cloud Platform (GCP) Compute offers a range of services that allow you to run your applications on Google's infrastructure. These services include:

These are key components of Google Cloud Platform's compute services:

1. Google Compute Engine (GCE): This is Google's Infrastructure as a Service (IaaS) that allows users to launch virtual machines (VMs) on demand. GCE provides a scalable and flexible environment for running your applications. You can choose from predefined machine types or customize your own to fit your needs.

2. AppEngine: This is a Platform as a Service (PaaS) that provides a fully managed serverless platform for developing and hosting web applications. With AppEngine, Google handles the management of the infrastructure so you can focus on your application code.

3. Managed container services: Google provides several services for managing and deploying containerized applications. These include:
    - Google Container Registry (GCR): A private Docker image storage on Google Cloud.
    - Google Kubernetes Engine (GKE): A managed environment for deploying, scaling, and managing containerized applications using Google infrastructure.
    - Cloud Run: A service that takes your containers and makes them invocable via HTTP requests. It is built from Knative, letting you choose to run your containers either fully managed with Cloud Run, or in your Google Kubernetes Engine cluster with Cloud Run on GKE.

4. Cloud Build: This is a service that executes your builds on Google Cloud Platform infrastructure. It can import source code from Google Cloud Storage, Cloud Source Repositories, GitHub, or Bitbucket, execute a build to your specifications, and produce artifacts such as Docker containers or Java archives.

# Questions
1. What are GCE instances?
2. How to add custom provisioning logic on VM start?
3. What options does Google provide in terms of cost saving for GCE? (committed usage, preemptive)
4. How to optimize app performance with AppEngine integration?
5. How to configure scale up/down GCE machines based on load/demand, what are the best practices, proactive scaling, etc?
6. How to migrate from on-prem to GCE?
7. How to push your image to GCR?
8. How to deploy your app to GKE?
9. What are available options to monitor Google compute services?

# Answers
1. GCE instances are virtual machines that run on Google's infrastructure. They can be customized to fit your computational needs and can be used to deploy, run, and scale your applications.

2. Custom provisioning logic on VM start can be added using startup scripts. These scripts run during the startup process of your instances and can be used to install software, configure settings, etc.

3. Google provides several options for cost saving on GCE. These include committed use contracts, which offer discounted prices in return for committing to use a specific instance type in a specific region for a certain period, and preemptible VMs, which are significantly cheaper but can be stopped by Google at any time.

4. App performance can be optimized with AppEngine by taking advantage of its automatic scaling, which adjusts the number of instances based on the load, and its support for multiple runtime environments and frameworks.

5. Scaling up/down GCE machines based on load/demand can be achieved using managed instance groups and autoscaling policies. Best practices include setting appropriate CPU utilization targets and ensuring that your application can handle changes in the number of instances.

6. Migration from on-prem to GCE can be achieved using tools like Migrate for Compute Engine, which automates the process of creating and managing VM instances.

7. You can push your image to GCR using the Docker command-line tool. The 'docker push' command is used to push an image to the GCR.

8. Deploying your app to GKE involves creating a Kubernetes deployment configuration that specifies the Docker image to use, the number of replicas, and other settings. This configuration is then applied using the 'kubectl apply' command.

9. Google provides several options to monitor compute services. These include Cloud Monitoring for collecting metrics, events, and metadata, Cloud Logging for storing, searching, analyzing, monitoring, and alerting on log data and events, and Cloud Trace for analyzing the latency of your application.