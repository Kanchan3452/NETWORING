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
