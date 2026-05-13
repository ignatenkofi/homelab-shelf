## Stage 1 - local forwarding: 

When a node receives BUM traffic, it floods the packet locally to all ports that are members of the same VLAN - just like in a traditional (non-MLAG) setup. Additionally, it forwards the traffic over the peer-port to the other MLAG node. 

**==> picture [13 x 13] intentionally omitted <==**

Forwarding over peer-port only happens if the peer-port is also a member of the VLAN. This is why documentation emphasizes that the peerport should be included in all VLANs that span both MLAG nodes.
