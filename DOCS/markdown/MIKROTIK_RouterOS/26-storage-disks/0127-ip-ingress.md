## IP ingress 

When a router first introduces a label (or labels) on an IP packet, and the resulting packet size including MPLS labels exceeds MPLS MTU, the router behaves as if interface MTU was exceeded - either fragment packet in fragments that do not exceed MPLS MTU when labels are attached (if IP Don't Fragment is not set) or generate ICMP Need Fragmentation error that is sent back to the originator.
