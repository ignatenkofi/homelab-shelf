## Neighbor discovery 

Sub-menu: `/ipv6 nd` 

In this submenu, IPv6 Neighbor Discovery (ND) protocol is configured. 

Neighbor Discovery (ND) is a set of messages and processes that determine relationships between neighboring nodes. ND, compared to IPv4, replaces Address Resolution Protocol (ARP), Internet Control Message Protocol (ICMP) Router Discovery, and ICMP Redirect and provides additional functionality. 

ND is used by hosts to: 

Discover neighboring routers. 

Discover addresses, address prefixes, and other configuration parameters. 

ND is used by routers to: 

Advertise their presence, host configuration parameters, and on-link prefixes. 

Inform hosts of a better next-hop address to forward packets to a specific destination. 

ND is used by nodes to: 

Both resolve the link-layer address of a neighboring node to which an IPv6 packet is being forwarded and determine when the link-layer address of a neighboring node has changed. 

Determine whether IPv6 packets can be sent to and received from a neighbor.
