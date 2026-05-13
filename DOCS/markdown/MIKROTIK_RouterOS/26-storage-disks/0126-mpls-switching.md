## MPLS Switching 

If the packet with labels included is bigger than MPLS MTU, MPLS tries to guess the protocol that is carried inside the MPLS frame: 

If this is an IP packet, MPLS produces an ICMP Need Fragment error. This behavior mimics IP protocol behavior. Note that this ICMP error is not routed back to the originator of a packet but is switched towards the end of LSP so that the egress router can route it back. 

If this is not an IP packet, MPLS simply drops it, because it does not know how to interpret the contents of the packet. This feature is very important in situations where MPLS applications such as VPLS are used (where frames that are MPLS tagged are not IP packets, but e.g. encapsulated Ethernet frames as in the case of VPLS) - if somewhere along the LSP MPLS MTU will be less than packet size prepared by ingress router, frames will simply get dropped.
