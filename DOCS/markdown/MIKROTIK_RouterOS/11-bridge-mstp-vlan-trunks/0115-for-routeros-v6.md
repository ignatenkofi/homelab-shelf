## For RouterOS v6: 

When bridge `vlan-filtering` is enabled, received untagged packets might get encapsulated into the VLAN header before the "DST-NAT" block, which means these packets can be filtered using the `mac-protocol=vlan` and `vlan-encap` settings. Encapsulation can happen if the outgoing interface has `frame-types` set to `admit-all` or `admit-only-untagged-and-priority-tagged` . Tagged packets might get decapsulated on the "BRIDGING DECISION" block, which means these packets will no longer match the `macprotocol=vlan` and `vlan-encap` settings. Decapsulation can happen if the packet's VLAN ID matches the outgoing port's untagged VLAN membership. 

For RouterOS v7 and newer: 

When bridge `vlan-filtering` is enabled, received untagged packets might get encapsulated into the VLAN header on the "BRIDGINGDECISION" block, which means these packets can be filtered using the `mac-protocol=vlan` and `vlan-encap` settings.  Encapsulation can happen if the outgoing interface has `frame-types` set to `admit-all` or `admit-only-untagged-and-priority-tagged` . Tagged packets might get decapsulated on the "BRIDGING DECISION" block, which means these packets will no longer match the `macprotocol=vlan` and `vlan-encap` settings. Decapsulation can happen if the packet's VLAN ID matches the outgoing port's untagged VLAN membership. 

Bridge Input 

677 

Bridge input is a process that takes place when a packet is destined for the bridge interface. Most commonly this happens when you need to reach some services that are running on the bridge interface (e.g. a DHCP server) or you need to route traffic to other networks. The very first steps are similar to the bridge forward process - after receiving a packet on the in-interface, the device determines that the in-interface is a bridge port, so it gets passed through the bridging process: 

1.  A packet goes through the bridge NAT dst-nat chain, where MAC destination and priority can be changed, apart from that, a packet can be simply accepted, dropped, or marked; 

2.  Checks whether the use-ip-firewall option is enabled in the bridge settings; 

3.  Run packet through the bridge host table to make a forwarding decision. A packet where the destination MAC address matches the bridge MAC address will be passed to the bridge input chain. A packet that ends up being flooded (e. 

   - g. broadcast, multicast, unknown unicast traffic), also reaches the bridge input chain as the bridge interface itself is one of the many destinations; 

4.  A packet goes through the bridge filter input chain, where priority can be changed or the packet can be simply accepted, dropped, or marked; 

**==> picture [505 x 424] intentionally omitted <==**
