## Stage 2 - remote forwarding by peer: 

When the peer node receives the BUM traffic over the peer-port, it floods the traffic to all regular bridge ports that are members of the same VLAN. These are ports that do not have an `mlag-id` specified (i.e., standalone Ethernet or bond interfaces). For `mlag-id` bond interfaces, the peer node makes a decision based on link status: 

If both links (local and remote) are active, it does not flood the traffic to its own MLAG bond port - this avoids sending duplicate packets since the first node has already handled that. 

If the remote peer’s link is inactive, and the local is active, the peer node will flood the traffic to the MLAG bond to ensure delivery. 

777 

The unicast traffic behaves similarly, but there is one key difference when comparing regular LAG with MLAG. In regular LAG setup, outgoing packets are load-balanced across all active links based on the transmit hash policy. In MLAG setups with both links active, traffic is not load-balanced across the peerport between the two switches. Instead, traffic is forwarded only through the local member links of the MLAG - it always takes the shortest path. The peerport is used only if the local MLAG link fails. In that case, traffic is forwarded to the other node via the peer-port to reach the destination. When this happens, the host table also updates the MAC address entries learned on MLAG bonds to indicate that the destination is now reachable via the peerport. In setups where MLAG bonds consist of 2 + 2 active links (2 links per node), the transmit hashing is performed only among the two local links - not across all four links. Load balancing can be achieved when MLAG pair is used for multiple dual-connected bonds and the incoming traffic is already distributed across both pairs.
