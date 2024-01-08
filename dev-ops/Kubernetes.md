# Kubernetes
1. Architecture of Kubernetes: Kubernetes follows a master-worker architecture. The master node is responsible for the management of the Kubernetes cluster, while the worker nodes run the actual applications.

    - Master Node: The master node (also known as the control plane) consists of various components such as the API Server, Controller Manager, Scheduler, and etcd. The API Server acts as the front-end for Kubernetes, the Controller Manager runs the controllers, the Scheduler schedules the tasks, and etcd is a consistent and highly-available key-value store used as Kubernetes' backing store for all cluster data.

    - Worker Nodes: The worker nodes run the actual applications and workloads. Each worker node has multiple components like the kubelet, kube-proxy, and the Container Runtime (like Docker).

2. Kubernetes Components: Kubernetes has several key components:

    - Pods: The smallest and simplest unit in the Kubernetes object model that you create or deploy. A Pod represents a running process on your cluster.

    - Services: An abstract way to expose an application running on a set of Pods as a network service.

    - Volumes: A directory containing data, accessible to the containers in a pod.

    - Namespaces: Virtual clusters backed by the same physical cluster.

    - Deployments: Provides declarative updates for Pods and ReplicaSets.

3. Configuration Management in Kubernetes Cluster: Kubernetes provides several resources for managing configurations:

    - ConfigMaps: Allows you to decouple configuration artifacts from image content to keep containerized applications portable.

    - Secrets: Used to store sensitive information like passwords, OAuth tokens, and ssh keys.

4. Container Management: Kubernetes uses a Container Runtime Interface (CRI) to interact with the container runtime (like Docker or containerd) that runs on a node. The kubelet on each node interacts with the container runtime to start/stop containers, pull container images, and so on. Kubernetes also provides features like health checks, resource limits, and environment variables for managing containers.
# Questions
1. Describe high level architecture of kubernetes cluster.
2. What is etcd and how it used by kubernetes?
3. Explain difference between node and pod?
4. What is namespace?
5. What is kube-proxy?
6. What is kubectl?
7. What is ReplicaSet?
8. What is Ingress controller? Explain usecases
9. What developer should do to deploy container and make it available from outside?
10. How to run kubernetes locally? MiniKube, Docker Kubernetes
11. Explain the difference between ClusterIP, NodePort, LoadBalancer and External Name.
12. How service discovery works in kubernetes?
13. What are config maps and secrets?
14. What are liveness and readiness probes?
15. What is labels and their purpose?
16. How to tell kubernetes to run your container on specific nodes (e.g. node with SSD)?
17. How to specify the amount of resources that need to be allocated to a container in Kubernetes?
18. What is storage provisioning? How to mount storage to your pod?
19. How to debug your code in kubernetes cluster?
20. How to configure auto scaling for your pod?
21. What is Helm? Describe its pros/cons and usecases.
22. What is helm charts? How they help managing your cluster? Alternatives?
23. Deployment strategies supported by kubernetes?
24. How to implement graceful shutdown for your containers?
25. Explain deployment pipeline. form deployment till container is up on the node?
26. What is kube-proxy. Explain kube-proxy modes:
27. IPVC proxy mode,User space mode, Iptable mode
# Answers
1. Kubernetes follows a master-worker architecture. The master node (also known as the control plane) consists of various components such as the API Server, Controller Manager, Scheduler, and etcd. The worker nodes run the actual applications and workloads.

2. etcd is a consistent and highly-available key-value store used as Kubernetes' backing store for all cluster data. It stores the configuration data of the cluster, representing the state of the cluster at any given point of time.

3. A node is a worker machine in Kubernetes, which can be either a virtual or a physical machine, depending on the cluster. Each node contains the services necessary to run Pods. A Pod is the smallest and simplest unit in the Kubernetes object model that you create or deploy. A Pod represents processes running on your cluster.

4. A Namespace is a way to divide cluster resources between multiple users. It provides a scope for names and can be used to provide multi-tenancy in a Kubernetes cluster.

5. kube-proxy is a network proxy that runs on each node in your cluster, maintaining network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster.

6. kubectl is a command line interface for running commands against Kubernetes clusters.

7. A ReplicaSet is a core concept in Kubernetes that maintains a stable set of replica Pods running at any given time.

8. An Ingress Controller is a Kubernetes resource that routes traffic from outside your cluster to services within the cluster. Use cases include providing HTTP routing, load balancing, and SSL termination.

9. To deploy a container and make it available from outside, a developer would need to create a Deployment or a Pod, and then expose it using a Service or an Ingress.

10. To run Kubernetes locally, you can use tools like Minikube or Docker Desktop. Minikube runs a single-node Kubernetes cluster inside a VM on your laptop. Docker Desktop allows you to run a Kubernetes cluster on your local machine alongside Docker.

11. ClusterIP, NodePort, LoadBalancer, and ExternalName are types of Services in Kubernetes. ClusterIP exposes the Service on a cluster-internal IP, NodePort exposes the Service on each Node’s IP at a static port, LoadBalancer exposes the Service externally using a cloud provider’s load balancer, and ExternalName maps the Service to the contents of the externalName field.

12. Service discovery in Kubernetes is typically handled by kube-dns/coredns. Services within a Kubernetes cluster can find each other and connect using the service name.

13. ConfigMaps and Secrets are Kubernetes objects that allow you to separate your application code from your configuration. ConfigMaps are used to store non-confidential data, while Secrets are used to store sensitive data.

14. Liveness and readiness probes are used in Kubernetes to check the health of your applications. Liveness probes are used to know when to restart a container, and readiness probes are used to know when a container is ready to start accepting traffic.

15. Labels are key/value pairs that are attached to objects, such as Pods. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users.

16. To run your container on specific nodes, you can use nodeSelector to specify a set of key-value pairs that must be present as labels on the node.

17. To specify the amount of resources that need to be allocated to a container in Kubernetes, you can use the resources field in the container spec to set requests (the minimum amount of resources) and limits (the maximum amount of resources).

18. Storage provisioning in Kubernetes involves creating PersistentVolumes and PersistentVolumeClaims. A PersistentVolume (PV) is a piece of storage in the cluster, and a PersistentVolumeClaim (PVC) is a request for storage by a user.

19. To debug your code in a Kubernetes cluster, you can use `kubectl logs` to access the logs for a container in a Pod, `kubectl exec` to execute a command in a container, or `kubectl port-forward` to forward a local network port to a port in the Pod.

20. To configure auto scaling for your pod, you can use the Horizontal Pod Autoscaler, which automatically scales the number of Pods in a replication controller, deployment, replica set or stateful set based on observed CPU utilization.

21. Helm is a package manager for Kubernetes. It allows developers and operators to package, configure, and deploy applications and services onto Kubernetes clusters. Helm is useful for the deployment, scaling, and upgrading of applications on Kubernetes.

22. Helm charts are packages of pre-configured Kubernetes resources. They help managing your cluster by providing a way to templatize your deployments, allowing you to parameterize your configurations and re-use them across your environments.

23. Kubernetes supports several deployment strategies, including Recreate (all existing Pods are killed before new ones are created), RollingUpdate (the deployment updates the Pods in a rolling update fashion), Blue-Green (two environments are maintained, one is live and one is idle), and Canary (release a new version to a subset of users, then proceed with a full rollout).

24. To implement graceful shutdown for your containers, you can catch the SIGTERM signal sent by Kubernetes and perform the necessary cleanup and shutdown procedures in your application.

25. The deployment pipeline in Kubernetes typically involves building a Docker image, pushing it to a registry, creating a Deployment to run the image, and exposing the Deployment with a Service or Ingress.

26. kube-proxy is a network proxy that runs on each node in your cluster, maintaining network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster. kube-proxy can run in one of three modes: userspace, iptables, or IPVS. Userspace mode is the oldest and slowest. Iptables mode is faster than userspace but can be CPU-intensive. IPVS mode is the newest and is generally the best choice for large clusters.

27. IPVS (IP Virtual Server) mode creates a load balancer inside the Linux kernel to distribute network traffic. It's faster and more scalable than the other modes. Userspace mode proxies traffic from a userspace process, while iptables mode proxies traffic using Linux netfilter rules.