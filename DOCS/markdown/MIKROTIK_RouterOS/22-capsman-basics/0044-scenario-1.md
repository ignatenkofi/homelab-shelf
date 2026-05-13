## Scenario #1 

In case, you already have a DHCP-server in the topology that is responsible for providing IP addresses to the network, and you want to install the AP behind it: 

1368 

**==> picture [505 x 234] intentionally omitted <==**

1.  Ensure that the AP has a bridge interface added and that all Ethernet and WiFi ports are a part of it. 2.  Setup DHCP-client on that bridge or, statically, add an IP address and a default route, instead. 3.  Change interface list members roles if required.
