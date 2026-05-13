## Protocol Overview 

782 

**==> picture [504 x 505] intentionally omitted <==**

The purpose of the VRRP is to communicate to all VRRP routers associated with the Virtual Router ID and support router redundancy through a prioritized election process among them. 

All messaging is done by IPv4 or IPv6 multicast packets using protocol 112 (VRRP). The destination address of an IPv4 packet is 224.0.0.18 and for IPv6 it is FF02:0:0:0:0:0:0:12. The source address of the packet is always the primary IP address of an interface from which the packet is being sent. In IPv6 networks, the source address is the link-local address of an interface. 

These packets are always sent with TTL=255 and are not forwarded by the router. If for any reason the router receives a packet with lower TTL, a packet is discarded. 

Each VR node has a single assigned MAC address. This MAC address is used as a source for all periodic messages sent by Master. 

Virtual Router is defined by VRID and mapped set of IPv4 or IPv6 addresses. The master router is said to be the owner of mapped IPv4/IPv6 addresses. There are no limits to using the same VRID for IPv4 and IPv6, however, these will be two different Virtual Routers. 

Only the Master router is sending periodic Advertisement messages to minimize the traffic. A backup will try to preempt the Master only if it has the higher priority and preemption is not prohibited. 

783 

**==> picture [13 x 13] intentionally omitted <==**

All VRRP routers belonging to the same VR must be configured with the same advertisement interval. If the interval does not match router will discard the received advertisement packet.
