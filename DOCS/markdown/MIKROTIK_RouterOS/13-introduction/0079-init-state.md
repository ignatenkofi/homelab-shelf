## Init state 

The purpose of this state is to wait for a Startup event. When this event is received, the following actions are taken: 

if priority is 255, 

- for IPv4 send advertisement packet and broadcast ARP requests; 

- for IPv6 send an unsolicited ND Neighbor Advertisement for each IPv6 address associated with the virtual router and set target address to linklocal address associated with VR; 

- transit to MASTER state; 

else transit to BACKUP state.
