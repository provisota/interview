# Networking
Networking in GCP involves the use of Virtual Private Cloud (VPC) for provisioning your private, isolated Google Cloud resources. Subnets are subdivisions of the IP range of a VPC network. Firewall rules in GCP control traffic to and from instances based on the instance's IP address, protocol, and port. Routing rules direct network traffic from an instance's network interface to a destination. Shared VPC allows an organization to connect resources from multiple projects to a common VPC network. Host project is the project that the shared VPC network resides in, and service projects are projects that have been attached to the host project. Cloud DNS is a scalable, reliable and managed authoritative Domain Name System (DNS) service running on the same infrastructure as Google. VPN in GCP provides secure access to your cloud resources. BGP sessions with VPN and CloudRouter allow dynamic routes with your non-Google network. Load balancing involves distributing network traffic across multiple servers to ensure no single server bears too much demand.

1. VPC (Virtual Private Cloud) and Subnets: VPC is a global resource that provides networking functionality to your cloud-based resources. It consists of a list of regional virtual subnetworks (subnets) in data centers, all connected by a global wide area network.

2. Firewall rules and routing: Firewall rules in GCP control traffic to and from instances based on the instance's IP address, protocol, and port. Routing rules direct network traffic from an instance's network interface to a destination.

3. Shared VPC (XPN) and Host/Service projects: Shared VPC allows an organization to connect resources from multiple projects to a common VPC network. The host project is the project that the shared VPC network resides in, and service projects are projects that have been attached to the host project.

4. Cloud DNS: Cloud DNS is a scalable, reliable, and managed authoritative Domain Name System (DNS) service running on the same infrastructure as Google.

5. VPN and BGP sessions with VPN and CloudRouter: VPN in GCP provides secure access to your cloud resources. BGP (Border Gateway Protocol) sessions with VPN and CloudRouter allow dynamic routes with your non-Google network.

6. Load Balancing: Load balancing involves distributing network traffic across multiple servers to ensure no single server bears too much demand. GCP supports several types of Load Balancers such as HTTP(S) Load Balancing, TCP/SSL Proxy Load Balancing, Network Load Balancing, and Internal TCP/UDP Load Balancing. The hierarchy includes external (global) and internal (regional) load balancing, and proxying is supported by some types of load balancers.

# Questions
1. What are the default and custom VPC firewall rules in GCP?
2. What types of Load Balancers does GCP support?
3. Which Load Balancers support session affinity and how is it achieved?
4. Can you describe the components and flow of an HTTPS Load Balancer?
5. What model does an Internal Load Balancer use (proxied/non-proxied, andromeda network)?
6. How can you communicate with an Internal Load Balancer that has an ephemeral IP?
7. How can you achieve fast dynamic IP resolving on both on-premises and VPC sides when using VPN?

# Answers
1. By default, GCP firewall rules block all incoming traffic to instances and allow all outgoing traffic. Custom firewall rules can be created to allow specific protocols and ports for incoming and outgoing traffic.
2. GCP supports several types of Load Balancers such as HTTP(S) Load Balancing, TCP/SSL Proxy Load Balancing, Network Load Balancing, and Internal TCP/UDP Load Balancing.
3. HTTP(S) Load Balancing and Internal TCP/UDP Load Balancing support session affinity which can be achieved by setting the sessionAffinity field to "CLIENT_IP" or "GENERATED_COOKIE".
4. An HTTPS Load Balancer consists of one or more forwarding rules, target proxies, URL maps, backend services, and backends. The flow starts with a client sending a request, the forwarding rule directs the request to a target proxy, which uses the URL map to route the request to a backend service, which then sends the request to a backend that is selected based on the configured load balancing algorithm.
5. An Internal Load Balancer uses the non-proxied model and is based on Andromeda, Google's network virtualization stack.
6. To communicate with an Internal Load Balancer that has an ephemeral IP, you can use the internal DNS name of the Load Balancer.
7. Fast dynamic IP resolving on both on-premises and VPC sides when using VPN can be achieved by using Cloud DNS and configuring DNS forwarding between your on-premises network and your VPC network.