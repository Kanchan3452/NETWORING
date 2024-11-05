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

## CNI (Container Network Interface)
A CNI plugin is responsible for inserting a network interface into the container network namespace (e.g., one end of a virtual ethernet (veth) pair) and making any necessary changes on the host(e.g., attaching the other end of the veth into a bridge). CNI is used by container runtimes, such as Kubernetes, as well as Podman, CRI-O, Mesos, and others.


## Flannel
Flannel is a simple and easy way to configure a layer 3 network fabric designed for Kubernetes.Flannel runs a small, single binary agent called flanneld on each host, and is responsible for allocating a subnet lease to each host out of a larger, preconfigured address space. Flannel uses either the Kubernetes API or etcd directly to store the network configuration, the allocated subnets. Packets are forwarded using one of several backend mechanisms including VXLAN and various cloud integrations.


**Networking in the cloud is a critical aspect of cloud computing that enables communication between various resources, services, and applications hosted in cloud environments. Here are some key concepts and components involved in cloud networking:**

**1)Virtual Private Cloud (VPC)**

A VPC allows you to create a logically isolated network within a cloud provider's infrastructure. You can define your own IP address range, subnets, route tables, and network gateways.

**2) Subnetting**
Subnetting is the process of dividing a large network into smaller networks called as “subnets.” Subnets provides each group of devices have thier own space to communicate, that ultimately helps network to work easily.

## INTERNET GATEWAY 
Internet Gateways. An internet gateway is a horizontally scaled, redundant, and highly available VPC component 

that allows communication between instances in your VPC and the internet. It therefore imposes no availability risks or 

bandwidth constraints on your network traffic.

## VIRTUAL PRIVATE GATEWAY 
It can be a physical or software appliance. The anchor on the AWS side of the VPN connection is called a virtual private gateway. The following diagram shows your network, the customer gateway, the VPN connection that goes to 
the virtual private gateway, and the VPC.

## ROUTE TABLE
Route Tables. A route table contains a set of rules, called routes that are used to determine where network traffic is directed. Each subnet in your VPC must be associated with a route table; the table controls the routing for the 
subnet.

## Elastic Load Balancing (ELB)
is a load-balancing service for Amazon Web Services (AWS) deployments. ELB automatically distributes incoming application traffic and scales resources to meet traffic demands.
