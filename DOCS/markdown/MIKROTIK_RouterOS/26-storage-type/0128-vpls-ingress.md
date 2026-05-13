## VPLS ingress 

When the router encapsulates the Ethernet frame for forwarding over VPLS pseudowire, it checks if packet size with VPLS Control Word (4 bytes) and any necessary labels (usually 2 labels - 8 bytes), exceeds MPLS MTU of the outgoing interface. If it does, VPLS fragments packets so that it honors the MPLS MTU of the outgoing interface. A packet is defragmented at the egress point of the VPLS pseudowire.
