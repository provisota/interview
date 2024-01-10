# Systems and Networking Fundamentals

## Basic Concepts of Networking

Networking fundamentals encompass the key concepts, technologies, and protocols that enable communication between
computers and other devices.

- **TCP/IP Model**: The primary suite of protocols used for communication over the internet, consisting of the
  [Internet Protocol](communication-protocols.md#internet-protocol-ip) (IP) for addressing and routing, and the
  [Transmission Control Protocol](communication-protocols.md#transmission-control-protocol-tcp) (TCP) for reliable data
  transfer.
- **[OSI Model](osi-model.md)**: A seven-layer framework that standardizes communications functions and is used for
  troubleshooting networking issues.
- **Routers and Switches**: Hardware devices that direct network traffic. Routers work at the network layer and
  direct traffic between different networks. Switches work at the data link layer and connect devices within the
  same network.
- **[DNS](dns.md) (Domain Name System)**: Translates domain names into IP addresses.
- **[DHCP](dhcp.md) (Dynamic Host Configuration Protocol)**: Assigns IP addresses to devices on a network.

## Key Networking Protocols

Understanding the role and functionality of various networking protocols is essential for network operation and
troubleshooting.

- **HTTP/HTTPS**: Protocols for transmitting web data.
- **FTP**: Used for transferring files between a client and a server.
- **SSH (Secure Shell)**: Provides a secure channel over an unsecured network, mainly used for logging into and
  executing commands on remote machines.
- **SMTP, IMAP, POP3**: Protocols used for sending and receiving emails.

## Q&A

### What is the difference between TCP and UDP, and how do you choose which one to use?

[TCP](communication-protocols.md#transmission-control-protocol-tcp) (Transmission Control Protocol) and
[UDP](communication-protocols.md#user-datagram-protocol-udp) (User Datagram Protocol) are both transport layer
protocols. TCP is connection-oriented, ensuring reliable and ordered delivery of data. It's used when data integrity and
reliability are more important than speed, such as in web browsing and email. UDP is connectionless, offering faster
transmission but with no guarantee of reliability or order. It is suitable for applications where speed is critical and
some data loss is acceptable, such as in video streaming or online gaming.

### How does a router differ from a switch in a network?

A router and a switch operate at different layers of the OSI model and serve different purposes. A router,
operating at the network layer, routes data between different networks, managing traffic between them and often
connecting a local network to the internet. A switch, operating at the data link layer, connects devices within the same
network (like computers within an office) and directs data to its destination within this network based on MAC
addresses.

### Can you explain how DNS works in a typical web browsing scenario?

When a user enters a website URL in their browser, the browser first contacts a DNS server to resolve the
domain name into an IP address. The DNS lookup involves querying different DNS servers, starting from the root DNS
servers to the TLD (Top-Level Domain) servers, and then to the authoritative DNS servers for the domain. Once the IP
address is obtained, the browser can initiate a connection to the web server hosting the website using the IP address.