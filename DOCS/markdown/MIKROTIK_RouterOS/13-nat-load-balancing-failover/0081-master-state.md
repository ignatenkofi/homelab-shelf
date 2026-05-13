## Master state 

When the MASTER state is set, the node functions as a forwarding router for IPv4/IPv6 addresses associated with the VR. 

In IPv4 networks, the Master node responds to ARP requests for the IPv4 address associated with the VR. In IPv6 networks Master node: 

responds to ND Neighbor Solicitation message for the associated IPv6 address; 

786 

sends ND Router Advertisements for the associated IPv6 addresses. 

If the advertisement packet is received by master node: 

If priority is 0, send advertisement immediately; 

If priority in advertisement packet is greater than nodes priority then transit to the backup state; 

If priority in advertisement packet is equal to nodes priority and primary IP Address of the sender is greater than the local primary IP Address, then transit to the backup state; Ignore advertisement in other cases. 

When the shutdown event is received, send the advertisement packet with priority=0 and transit to Init state.
