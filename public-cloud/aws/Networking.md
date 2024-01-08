# Networking
1. **Virtual Private Cloud (VPC) and Subnets**: A VPC is a virtual network dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS Cloud. You can launch your AWS resources, such as Amazon EC2 instances, into your VPC. A subnet is a range of IP addresses in your VPC. You can launch AWS resources into a subnet that you select.

2. **Security Groups (SG) vs Network Access Control Lists (ACL)**: Security Groups act as a virtual firewall for your instance to control inbound and outbound traffic. Network ACLs act as a firewall for associated subnets, controlling both inbound and outbound traffic at the subnet level.

3. **Route53**: Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. It is designed to give developers and businesses an extremely reliable and cost-effective way to route end users to Internet applications.

4. **DirectConnect**: AWS Direct Connect is a cloud service solution that makes it easy to establish a dedicated network connection from your premises to AWS.

5. **CloudFront**: Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds.

6. **VPC Endpoints**: A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.

7. **Load Balancing (ELB, ALB)**: Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses. Application Load Balancer (ALB) is best suited for load balancing of HTTP and HTTPS traffic and provides advanced request routing targeted at the delivery of modern application architectures.

8. **ApiGateway**: Amazon API Gateway is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale.

9. **Peering**: Amazon VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses.

10. **NAT**: Network Address Translation (NAT) devices enable instances in a private subnet to connect to the internet or other AWS services, but prevent the internet from initiating a connection with those instances.

11. **VPN**: AWS Virtual Private Network (VPN) solutions establish secure connections between your on-premises networks, remote offices, client devices, and the AWS global network.
# Questions
1. What are the properties of default VPC?
2. How to open port on the EC2 for connection?
3. How to allow connection from EC2 to RDS instance?
4. How to allow traffic of different VPCs?
5. What is VPC peering and what topology does it support?
6. Types of LoadBalancers, what is the difference between V4/V7?
7. What is the difference between CNAME and A record in route53?
8. What Route53 routing policy should be used to split traffic in exact proportion of 20%/80% traffic between 2 regions?
9. How integrate DC and AWS network and replicate data/ precache data on AWS/DC side?
10. How to guarantee network connection to services over private network (no public) ?
# Answers
1. A default VPC is a logically isolated virtual network in the AWS cloud that is automatically created for your AWS account when you create it. It is preconfigured with a sizeable IP address range, a default subnet in each Availability Zone, a default security group, a default network access control list (ACL), and a default route table.

2. To open a port on an EC2 instance, you need to modify the inbound rules of the security group associated with the instance. You can add a rule that allows traffic on the desired port from the desired source IP addresses.

3. To allow a connection from an EC2 instance to an RDS instance, both instances need to be in the same VPC or in peered VPCs. You also need to modify the security group associated with the RDS instance to allow inbound traffic on the database port from the EC2 instance.

4. To allow traffic between different VPCs, you can use VPC peering, which allows you to connect two VPCs and route traffic between them using private IPv4 addresses or IPv6 addresses.

5. VPC peering is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses. It supports star topology (one central VPC peers with multiple other VPCs) and mesh topology (every VPC peers with every other VPC).

6. AWS provides three types of load balancers: Application Load Balancer (Layer 7), Network Load Balancer (Layer 4), and Classic Load Balancer (both Layer 7 and Layer 4). Layer 7 load balancers route traffic based on the content of the request (e.g., URL, headers), while Layer 4 load balancers route traffic based on the source and destination IP addresses and ports.

7. In Route53, a CNAME record maps one domain name (an alias) to another domain name. An A record maps a domain name to an IPv4 address. The main difference is that a CNAME record can point to any DNS record (including another CNAME), while an A record can only point to an IP address.

8. To split traffic in an exact proportion of 20%/80% between two regions, you can use the Weighted routing policy in Route53. You can assign weights to different record sets to specify what portion of traffic goes to which record.

9. To integrate a data center (DC) and AWS network, you can use AWS Direct Connect or VPN. To replicate or cache data, you can use services like AWS DataSync (for file data) or Amazon RDS (for database data).

10. To guarantee network connection to services over a private network, you can use VPC endpoints. A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.