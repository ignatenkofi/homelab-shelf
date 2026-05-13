## Backup state 

When in the backup state, 

in IPv4 networks, a node is not responding to ARP requests and is not forwarding traffic for the IP associated with the VR. 

in IPv6 networks, a node is not responding to ND Neighbor Solicitation messages and is not sending ND Router Advertisement messages for VRassociated IPv6 addresses. 

Routers' main task is to receive advertisement packets and check if the master node is available. 

The backup router will transmit itself to the master state in two cases: 

If priority in advertisement packet is 0; 

When Preemption_Mode is set to yes and Priority in the ADVERTISEMENT is lower than the local Priority 

After the transition to Master state node is: 

in IPv4 broadcasts gratuitous ARP request; in IPv6 sends an unsolicited ND Neighbor Advertisement for every associated IPv6 address. 

In other cases, advertisement packets will be discarded. When the shutdown event is received, transit to Init state. 

**==> picture [13 x 13] intentionally omitted <==**

Preemption mode is ignored if the Owner router becomes available.
