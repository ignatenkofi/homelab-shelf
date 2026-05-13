## Connected Routes 

Connected routes represent the network on which hosts can be directly reached (direct attachment to Layer2 broadcast domain). These routes are created automatically for each IP network that has at least one enabled interface attached to it (as specified in the /ip address or /ipv6 address configuration). RIB tracks the status of connected routes but does not modify them. For each connected route there is one IP address item such that: 

- address part of the dst-address of the connected route is equal to a network of IP address item. 

- netmask part of dst-address of the connected route is equal to the netmask part of the address of the IP address item. gateway of the connected route is equal to the actual-interface of the IP address item (same as an interface, except for bridge interface ports) and represents an interface where directly connected hosts from the particular Layer3 network can be reached. 

**==> picture [13 x 13] intentionally omitted <==**

The preferred source is not used anymore for connected routes. FIB chooses the source address based on the out-interface. This allows making setups that in ROS v6 and older were considered invalid. See examples for more details. 

180
