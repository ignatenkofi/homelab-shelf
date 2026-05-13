## Terminology 

- NVO: Network Virtualization Overlay used to deliver Layer2 and Layer 3 VPN services. 

- NVE: Network Virtualization Endpoint is Provider Edge (PE) node within the NVO environment. It is responsible for encapsulation/decapsulation of VPN traffic. In case of VXLAN this defines VTEP (Virtual Tunnel End Point). 

- VNI: Virtual Network Identifier 

- EVI: EVPN Instance 

- RD: Route Distinguisher is a 64-bit prefix appended to IP prefix to make it unique, multiple tenants can use overlapping IP range. 

- RT: Route Target is BGP extended community used to control import and export of routes. Typically, RT is based on the AS number and the VNI of the MAC-VRF 

- MAC-VRF: VRF table for MAC addresses on a PE (VTEP). Requires RD and RT. 

BUM:  Broadcast, unknown Unicast and Multicast traffic is a multi-destination layer2 traffic in vxlan networks. 

Ingress replication: unicast approach to handle BUM traffic. It uses IMET routes to auto-discover remote peers.  Ingress device replicates BUM traffic to all the VTEPS associated with the Layer-2 VNI. 

- ESI - Ethernet Segment Identifier 

For MP-BGP to carry EVPN, new AFI/SAFI was defined 25(L2 VPN)/70(EVPN). Next-hop address within the NLRI is an IP address of the VTEP advertising the EVPN route. 

There are five EVPN route types: 

1022 

- Type-1: (Ethernet A-D) announces reachability of multi-homed ethernet segment 

- Type-2:( MAC advertisement MACIP) advertises MAC address of MAC/IP binding learned by specific EVI 

- Type-3: (Inclusive multicast IMET) advertises membership of a Layer 2 domain, allowing to auto discover VTEPs 

- Type-4: (Ethernet segment) is used to discover VTEPs attached to the same shared Ethernet Segment for EVPN multi-homing model (activeactive, active-standby forwarding) 

Type-5: (IP prefix) Advertising IP prefix into the EVPN domain allows to create classic Layer 3 VPN. 

Data plane encapsulation is defined with encapsulation extended community value: 

- 8 - VXLAN (currently only one supported by ROS) 

- 9 - NVGRE 

- 10 - MPLS 

- 11 - MPLSoGRE 

There are two methods for supporting inter-subnet routing with EVPN: symmetric and asymmetric integrated routing and bridging (IRB). The main difference between the two methods is that the symmetric method supports both routing and bridged on both the ingress and egress VTEPs, where the asymmetric method supports routing on the ingress, but only bridging on the egress.
