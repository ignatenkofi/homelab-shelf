## Label switching ICMP errors 

One of the drawbacks of using traceroute in MPLS networks is the way MPLS handles produced ICMP errors. In IP networks ICMP errors are simply routed back to the source of the packet that caused the error. In an MPLS network, it is possible that a router that produces an error message does not even have a route to the source of the IP packet (for example in the case of asymmetric label switching paths or some kind of MPLS tunneling, e.g. to transport MPLS VPN traffic). 

Due to this produced ICMP errors are not routed to the source of the packet that caused the error but switched further along the label switching path, assuming that when the label switching path endpoint will receive an ICMP error, it will know how to properly route it back to the source. 

848 

This causes the situation, that traceroute in MPLS network can not be used the same way as in IP network - to determine failure point in the network. If the label switched path is broken anywhere in the middle, no ICMP replies will come back, because they will not make it to the far endpoint of the label switching path.
