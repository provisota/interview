# Networking

## Virtual Networks
A Virtual Network, also known as a VNet, in Azure is a logically isolated section of the Azure cloud where you can launch Azure resources in a virtual network that you define.

## VPN Gateways
A VPN Gateway is a specific type of virtual network gateway that is used to send encrypted traffic between an Azure virtual network and an on-premises location over the public Internet.

## Network Security Groups
Network Security Groups (NSGs) in Azure are used to filter network traffic to and from Azure resources in an Azure virtual network. An NSG can contain multiple inbound and outbound security rules that enable you to filter traffic to and from resources by source and destination IP address, port, and protocol.

## Load Balancing
Load Balancing in Azure distributes inbound flows that arrive at the load balancer's front end to backend pool instances. These flows are according to configured load balancing rules and health probes.

## Front Door
Azure Front Door is a global, scalable entry-point that uses the Microsoft global edge network to create fast, secure, and widely scalable web applications or APIs.

## Traffic Manager
Azure Traffic Manager is a DNS-based traffic load balancer that enables you to distribute traffic optimally to services across global Azure regions, while providing high availability and responsiveness.

## Application Gateway
Azure Application Gateway is a web traffic load balancer that enables you to manage traffic to your web applications.

## Azure Load Balancer
Azure Load Balancer is a high-performance, ultra low-latency Layer 4 load-balancing service (TCP/UDP) for all UDP and TCP protocols.

## Questions
1. How to configure security rules for a VNET?
2. What types of VPN Gateways exist and when are they used?
3. How to connect two different VNETs?
4. What are the load balancing options in Azure? What is the difference, which of them are L4 and L7? What are the best scenarios for each of them?

## Answers
1. Security rules for a VNET can be configured using Network Security Groups (NSGs). These rules can be applied to a subnet within the VNET or directly to a VM.
2. There are two types of VPN Gateways in Azure: Route-based and Policy-based. Route-based gateways are used for point-to-site VPNs, inter-virtual network, and multi-site connections. Policy-based gateways are used for site-to-site connections only.
3. Two different VNETs can be connected using VNET peering or by using a VPN Gateway.
4. Azure provides several load balancing options including Azure Load Balancer for Layer 4 (TCP/UDP) and Azure Application Gateway for Layer 7 (HTTP/HTTPS). Azure Load Balancer is best for scenarios that require network level load balancing, while Azure Application Gateway is best for scenarios that require application level load balancing such as URL routing, cookie-based session affinity, and SSL offload.