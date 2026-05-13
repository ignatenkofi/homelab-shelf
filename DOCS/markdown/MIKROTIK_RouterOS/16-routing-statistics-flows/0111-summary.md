## Summary 

The Border Gateway Protocol (BGP) allows setting up an inter-domain dynamic routing system that automatically updates routing tables of devices running BGP in case of network topology changes. 

BGP is an inter-autonomous system routing protocol based on the distance-vector algorithm. It is used to exchange routing information across the Internet and is the only protocol that is designed to deal with a network of the Internet's size and the only protocol that can deal well with having multiple connections to unrelated routing domains. 

BGP is designed to allow for sophisticated administrative routing policies to be implemented. It does not exchange information about network topology but rather reachability information. As such, BGP is better suited to inter-AS environments and special cases like informational feeds. If you just need to enable dynamic routing in your network, consider OSPF instead. 

**==> picture [13 x 13] intentionally omitted <==**

The feature is not supported on SMIPS devices (hAP lite, hAP lite TC, and hAP mini). 

Standards and Technologies: 

RFC 4271 Border Gateway Protocol 4 RFC 4456 BGP Route Reflection 

RFC 5065 Autonomous System Confederations for BGP RFC 1997 BGP Communities Attribute RFC 8092 BGP Large Communities 

RFC 4360, 5668 BGP Extended Communities RFC 2385 TCP MD5 Authentication for BGPv4 RFC 5492 Capabilities Advertisement with BGP-4 RFC 2918 Route Refresh Capability 

RFC 4760 Multiprotocol Extensions for BGP-4 RFC 2545 Use of BGP-4 Multiprotocol Extensions for IPv6 Inter-Domain Routing RFC 4893 BGP Support for Four-octet AS Number Space 

- RFC 4364 BGP/MPLS IP Virtual Private Networks (VPNs) RFC 4761 Virtual Private LAN Service (VPLS) Using BGP for Auto-Discovery and Signalling RFC 6286 - AS-wide Unique BGP Identifier for BGP-4 RFC 4273 - SNMP peer table monitoring (OID 1.3.6.1.2.1.15.3.1) (IPv4 only) RFC 6793 -  4-byte ASN support and Aggregator attribute.
