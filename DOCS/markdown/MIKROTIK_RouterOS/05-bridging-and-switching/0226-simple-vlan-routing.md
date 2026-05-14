## Simple VLAN routing 

Let us assume that we have several MikroTik routers connected to a hub. Remember that a hub is an OSI physical layer device (if there is a hub between routers, then from the L3 point of view it is the same as an Ethernet cable connection between them). For simplification assume that all routers are connected to the hub using the ether1 interface and have assigned IP addresses as illustrated in the figure below. Then on each of them the VLAN interface is created. 

Configuration for R2 and R4 is shown below:
