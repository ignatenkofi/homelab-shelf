## Inter-VLAN Routing with Upstream Port Behind Firewall/NAT 

This example demonstrates how to benefit from near-to-wire-speed inter-VLAN routing while keeping Firewall and NAT running on the upstream port. Moreover, Fasttrack connections to the upstream port get offloaded to hardware as well, boosting the traffic speed close to wire-level. Inter-VLAN traffic is fully routed by the hardware, not entering the CPU/Firewall, and, therefore, not occupying the hardware memory of Fasttrack connections. 

We use the CRS317-1G-16S+ model with the following setup: 

sfp1-sfp4 - bridged ports, VLAN ID 20, untagged sfp5-sfp8 - bridged ports, VLAN ID 30, untagged sfp16 - the upstream port ether1 - management port 

Setup interface lists for easy access: 

443
