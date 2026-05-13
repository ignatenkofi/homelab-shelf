## Overview 

OSPF is Interior Gateway Protocol (IGP) designed to distribute routing information between routers belonging to the same Autonomous System (AS). 

The protocol is based on link-state technology that has several advantages over distance-vector protocols such as RIP: 

no hop count limitations; 

multicast addressing is used to send routing information updates; updates are sent only when network topology changes occur; the logical definition of networks where routers are divided into areas transfers and tags external routes injected into AS. 

However, there are a few disadvantages: 

OSPF is quite CPU and memory intensive due to the SPF algorithm and maintenance of multiple copies of routing information; more complex protocol to implement compared to RIP; 

RouterOS implements the following standards: 

- RFC 2328 - OSPF Version 2 RFC 3101 - The OSPF Not-So-Stubby Area (NSSA) Option RFC 3630 - Traffic Engineering (TE) Extensions to OSPF Version 2 RFC 4577 - OSPF as the Provider/Customer Edge Protocol for BGP/MPLS IP Virtual Private Networks (VPNs) RFC 5329 - Traffic Engineering Extensions to OSPF Version 3 RFC 5340 - OSPF for IPv6 RFC 5643 - Management Information Base for OSPFv3 RFC 6549 - OSPFv2 Multi-Instance Extensions RFC 6565 - OSPFv3 as a Provider Edge to Customer Edge (PE-CE) Routing Protocol RFC 6845 - OSPF Hybrid Broadcast and Point-to-Multipoint Interface Type RFC 7471 - OSPF Traffic Engineering (TE) Metric Extensions 

992
