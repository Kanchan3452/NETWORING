# NETWORKING

A computer network is a set of computers sharing resources located on or provided by network nodes. Computers use common communication protocols over digital interconnections to communicate with each other. These interconnections are made up of telecommunication network technologies based on physically wired, optical, and wireless radio-frequency methods that may be arranged in a variety of network topologies.

## Bridge
A Linux bridge behaves like a network switch. It forwards packets between interfaces that are connected to it. It's usually used for forwarding packets on routers, on gateways, or between VMs and network namespaces on a host. It also supports STP, VLAN filter, and multicast snooping.


## VLAN
A VLAN, aka virtual LAN, separates broadcast domains by adding tags to network packets. VLANs allow network administrators to group hosts under the same switch or between different switches.

## VXLAN
VXLAN (Virtual eXtensible Local Area Network) is a tunneling protocol designed to solve the problem of limited VLAN IDs (4,096) in IEEE 802.1q. It is described by IETF RFC 7348.
With a 24-bit segment ID, aka VXLAN Network Identifier (VNI), VXLAN allows up to 2^24 (16,777,216) virtual LANs, which is 4,096 times the VLAN capacity.

VXLAN is typically deployed in data centers on virtualized hosts, which may be spread across multiple racks.

## MACVLAN
With VLAN, you can create multiple interfaces on top of a single one and filter packages based on a VLAN tag. With MACVLAN, you can create multiple interfaces with different Layer 2 (that is, Ethernet MAC) addresses on top of a single one.

Before MACVLAN, if you wanted to connect to physical network from a VM or namespace, you would have needed to create TAP/VETH devices and attach one side to a bridge and attach a physical interface to the bridge on the host at the same time,.

## IPVLAN
IPVLAN is similar to MACVLAN with the difference being that the endpoints have the same MAC address.

![image](https://github.com/user-attachments/assets/dfa08e77-f351-4bf0-91a9-3fbf6e59c89b)

IPVLAN supports L2 and L3 mode. IPVLAN L2 mode acts like a MACVLAN in bridge mode. The parent interface looks like a bridge or switch.
In IPVLAN L3 mode, the parent interface acts like a router and packets are routed between endpoints, which gives better scalability.

Regarding when to use an IPVLAN, the IPVLAN kernel documentation says that MACVLAN and IPVLAN "are very similar in many regards and the specific use case could very well define which device to choose. if one of the following situations defines your use case then you can choose to use ipvlan -
(a) The Linux host that is connected to the external switch / router has policy configured that allows only one mac per port.
(b) No of virtual devices created on a master exceed the mac capacity and puts the NIC in promiscuous mode and degraded performance is a concern.
(c) If the slave device is to be put into the hostile / untrusted network namespace where L2 on the slave could be changed / misused."

## VETH
The VETH (virtual Ethernet) device is a local Ethernet tunnel. Devices are created in pairs, as shown in the diagram below.

Packets transmitted on one device in the pair are immediately received on the other device. When either device is down, the link state of the pair is down.

## VCAN
Similar to the network loopback devices, the VCAN (virtual CAN) driver offers a virtual local CAN (Controller Area Network) interface, so users can send/receive CAN messages via a VCAN interface. CAN is mostly used in the automotive field nowadays.

## VXCAN
Similar to the VETH driver, a VXCAN (Virtual CAN tunnel) implements a local CAN traffic tunnel between two VCAN network devices. When you create a VXCAN instance, two VXCAN devices are created as a pair. When one end receives the packet, the packet appears on the device's pair and vice versa. VXCAN can be used for cross-namespace communication.



## LINUX BRIDGE
A Linux bridge is a kernel module that behaves like a network switch, forwarding packets between interfaces that are connected to it. It's usually used for forwarding packets on routers, on gateways, or between VMs and network namespaces on a host.

## OPEN VIRTUAL SWITCH (OVS)
Open vSwitch (OVS) is an open-source implementation of a distributed virtual multilayer switch. The main purpose of Open vSwitch is to provide a switching stack for hardware virtualization environments, while supporting multiple protocols and standards used in computer networks.
![image](https://github.com/user-attachments/assets/101a121e-1d0f-4407-b913-e770249f3b5f)


## TUN/TAP
TUN, namely network TUNnel, simulates a network layer device and operates in layer 3 carrying IP packets. TUN is used with routing. 

 TAP, namely network TAP, simulates a link layer device and operates in layer 2 carrying Ethernet frames  TAP can be used to create a user space network bridge.

 ![image](https://github.com/user-attachments/assets/c8bf9fdb-fc1d-4e05-819d-ec1d23375fa5)

NETWORKING IN CLOUD--

![image](https://github.com/user-attachments/assets/48904026-ee26-427b-b2e9-4e3e97051baa)


**Networking in the cloud is a critical aspect of cloud computing that enables communication between various resources, services, and applications hosted in cloud environments. Here are some key concepts and components involved in cloud networking:**

**1)Virtual Private Cloud (VPC)**

A VPC allows you to create a logically isolated network within a cloud provider's infrastructure. You can define your own IP address range, subnets, route tables, and network gateways.

**2)Subnets**

Subnets are segments of a VPC that help organize and secure your cloud resources. They can be public (accessible from the internet) or private (accessible only from within the VPC).

**3)Load Balancer**

Load balancers distribute incoming traffic across multiple servers or resources, ensuring high availability and reliability of applications. They can be application-specific (Layer 7) or network-based (Layer 4).

**4)VPN and Direct Connect**

Virtual Private Networks (VPNs) create secure connections between your on-premises infrastructure and cloud resources. Direct Connect offers a dedicated network connection to the cloud provider, enhancing security and performance.

**5)Firewalls and Security Groups**

Cloud providers offer built-in firewalls and security groups to control inbound and outbound traffic. These tools help you define rules that specify which traffic is allowed or denied.

**6)Content Delivery Networks (CDN)**

CDNs cache content closer to users around the globe, improving access speed and performance for web applications.

**7)DNS Services**

Cloud-based DNS services manage domain names and route traffic efficiently to different resources, improving reliability and speed.

**8)Network Monitoring and Management**

Tools for monitoring network performance, tracking usage, and troubleshooting issues are essential for maintaining cloud network health

**9)TTL**

TTL, or Time to Live, in the context of cloud computing typically refers to the duration that data can exist in a cache or be considered valid before being refreshed or discarded. Here are a few contexts in which TTL is relevant:

---DNS Records: TTL determines how long a DNS resolver can cache a DNS record before it must query the authoritative server again. Shorter TTL values can lead to more frequent updates but increase the load on DNS servers.

---Caching: In cloud services (like AWS, Azure, or Google Cloud), TTL can define how long cached objects (such as those in a CDN or a caching layer) are considered fresh. This helps optimize performance by reducing the need to fetch data from the source frequently.

---Session Management: TTL can also be applied to session tokens or user sessions in web applications, dictating how long a session remains active before timing out for security reasons.

---Data Expiry: In databases or storage solutions, TTL can specify how long certain data should be retained before it is automatically deleted.

**10)CNI**

![image](https://github.com/user-attachments/assets/23323a8b-aa8e-48bf-8918-58627c65f400)


CNI stands for Container Network Interface. It's a specification and a set of libraries designed to facilitate the networking of containers in a cloud-native environment. CNI allows containers to communicate with each other and with external networks while ensuring network configuration is flexible and scalable.

**Key Concepts of CNI:**
---Plugins: CNI works through a series of network plugins that can be used to configure container networking. These plugins can handle tasks like assigning IP addresses, setting up routes, and configuring firewall rules.

---Decoupled Architecture: CNI separates network configuration from the container runtime, meaning that different container orchestrators (like Kubernetes, Mesos, or Docker Swarm) can use the same networking solutions.

---IP Address Management: CNI can allocate IP addresses to containers dynamically and manage their lifecycle, including handling IP address releases when containers are stopped.

---Network Isolation: CNI supports multiple network interfaces and allows for isolation between different applications or services by creating separate network namespaces.

---Integration with Orchestrators: Most modern container orchestration platforms, especially Kubernetes, utilize CNI to manage networking between pods.

**Common CNI Plugins:**

---Flannel: A simple overlay network that allows containers on different hosts to communicate.

---Calico: Offers both networking and network policy for containers.

---Weave Net: Provides a virtual network for containers that works across multiple hosts.

# MOVEMENT OF PACKETS

![image](https://github.com/user-attachments/assets/ab3d3fb6-7b14-4978-a9d1-6463d91b92a4)

The movement of packets in the cloud involves several layers and processes, ensuring that data can travel efficiently from one point to another, whether it's within a single data center or across a global network. Here’s a breakdown of how packets move in a cloud environment:

**1. Data Center Architecture:**

Physical Layer: At the base, there are physical servers and networking hardware (switches, routers).

Virtualization Layer: Virtual machines (VMs) and containers are created on these physical servers, abstracting the hardware and allowing for resource allocation and management.

**2. Networking Models:**

Overlay Networks: Many cloud providers use overlay networking to abstract the underlying physical network, allowing for easier management and scalability.

Software-Defined Networking (SDN): This enables centralized control of network traffic, allowing for dynamic adjustments based on load and demand.

**3. Packet Routing:**

Ingress/Egress Points: Packets enter and exit the cloud network through designated ingress (entry) and egress (exit) points. This could involve load balancers that distribute traffic among multiple servers.

Routing Protocols: Inside the cloud, various routing protocols (like BGP, OSPF) are used to determine the most efficient path for packet delivery.

**4. Transport Layer:**

TCP/UDP: Data packets are transported using protocols like TCP (for reliable, ordered communication) or UDP (for faster, connectionless communication). The choice depends on the application’s requirements.

**5. Security Measures:**

Firewalls and Security Groups: Packets are filtered at various points to enforce security policies. This could include virtual firewalls or security groups that control inbound and outbound traffic.

Encryption: Data packets may be encrypted in transit, particularly when moving between data centers or to/from end users, using protocols like TLS.

**6. Traffic Management:**

Load Balancing: Load balancers distribute incoming traffic across multiple servers to ensure no single server becomes a bottleneck.

![image](https://github.com/user-attachments/assets/fc8a771f-2fa0-47ba-9c02-e5b5926b8788)


Content Delivery Networks (CDNs): For static content, CDNs cache data at various locations to minimize latency and speed up delivery to end users.

**7. Monitoring and Logging:**

Network Monitoring: Tools and services monitor the flow of packets, helping to identify issues and optimize performance.

Logging: Activity logs help track packet movements and diagnose problems.

**8. Inter-Cloud Communication:**

Peering and Interconnection: Different cloud providers can connect through peering arrangements, allowing packets to traverse multiple clouds.

APIs: Cloud services often expose APIs that allow for data transfer between different services and applications, which involves packet movement across networks.

# IPV4

![image](https://github.com/user-attachments/assets/1ec608cc-1c51-4d2a-877d-bf372827382c)


IPv4, or Internet Protocol version 4, is one of the core protocols of the Internet Protocol Suite. It is primarily responsible for addressing and routing packets of data between devices on a network. Here are the key features and concepts related to IPv4:

**Key Features of IPv4:**

**Addressing:**

--32-bit Address Space: IPv4 uses a 32-bit address format, allowing for approximately 4.3 billion unique addresses (2^32). This is often represented in decimal as four octets (e.g., 192.168.1.1).

--Classes: IPv4 addresses are categorized into classes (A, B, C, D, and E) based on their leading bits, which affect the size of the network and host portions of the address.

**Subnetting:**

--Network and Host Portions: An IPv4 address consists of a network part (identifying the network) and a host part (identifying the specific device on that network). Subnetting allows for the division of a larger network into smaller, more manageable sub-networks.

--CIDR Notation: Classless Inter-Domain Routing (CIDR) allows for more flexible allocation of IP addresses. For example, 192.168.1.0/24 indicates a subnet with 256 addresses.
Packet Structure:

**An IPv4 packet consists of a header and a payload. The header includes information like the source and destination IP addresses, protocol type, and other control information.
The maximum transmission unit (MTU) defines the largest packet size that can be sent over the network.**

**Routing:**

![image](https://github.com/user-attachments/assets/058eced4-6598-4bce-ae3b-e7dd62bca642)

Routers use IPv4 addresses to determine the best path for forwarding packets across interconnected networks.
Routing protocols (like BGP, OSPF, and RIP) facilitate the dynamic exchange of routing information.

**Address Allocation:**

IPv4 addresses are managed and allocated by the Internet Assigned Numbers Authority (IANA) and regional Internet registries (RIRs).
Address exhaustion has led to the adoption of strategies like Network Address Translation (NAT) and private addressing.

**Private and Public Addresses:**

Certain IPv4 address ranges are designated for private use (e.g., 10.0.0.0 to 10.255.255.255, 192.168.0.0 to 192.168.255.255), which can be used internally within organizations.
Public addresses are routable on the Internet and are unique across the entire network.

**Limitations of IPv4:**

-Address Exhaustion: The finite address space has led to IPv4 address exhaustion, prompting the need for IPv6.

-Complexity with NAT: While NAT allows multiple devices to share a single public IP, it can complicate certain applications and protocols.

-Limited Security Features: IPv4 does not inherently include security features, leading to the need for additional protocols (like IPsec) for secure communication

-Transition to IPv6: Due to the limitations of IPv4, the Internet community has been transitioning to IPv6, which uses a 128-bit address space, vastly increasing the number of available addresses and incorporating features for improved security and efficiency.

---Cilium: Uses eBPF to provide advanced networking and security features.

# Key Concepts of a Bridge in Cloud Networking:

![image](https://github.com/user-attachments/assets/34adbce1-8e0b-475a-a5d5-a34c58eba8ac)


**Network Connectivity:**

A bridge connects two or more separate networks, allowing them to function as a single network. This can facilitate communication between virtual machines (VMs) in different subnets or virtual networks.

**Layer 2 Functionality:**

Bridges operate at Layer 2 of the OSI model (Data Link Layer). They use MAC addresses to forward packets to the appropriate destination within the connected networks, making decisions based on the data link layer information.

**Virtual Network Bridging:**

In a cloud environment, bridges can be used to link virtual networks created by different services or instances. For example, a bridge might connect a private network in a cloud provider's infrastructure with on-premises networks.

**Network Segmentation:**

Bridges can be used to segment traffic within a cloud environment, enhancing security and performance by isolating network segments while still allowing them to communicate when necessary.
Common Use Cases:

**Hybrid Cloud Connectivity:**

In hybrid cloud architectures, bridges can facilitate communication between on-premises data centers and cloud resources, allowing for seamless integration of workloads and data.
Microservices Communication:

In microservices architectures, different services might run in isolated environments. Bridges help connect these services, ensuring they can communicate effectively.
Multi-Cloud Environments:

When using multiple cloud providers, bridges can help interconnect services across these clouds, allowing data and workloads to flow freely.
VPN and Security:

Bridges can be part of a broader network security strategy, helping to connect secure networks or provide VPN access to resources in the cloud.

# Implementation in Cloud Providers:

-AWS: AWS offers Virtual Private Cloud (VPC) Peering, which allows for the creation of isolated networks that can be connected with bridges.

-Azure: Azure Virtual Network Peering enables communication between Azure virtual networks.

-Google Cloud: Google Cloud's VPC allows for network segmentation and the ability to connect different projects through VPC peering.
