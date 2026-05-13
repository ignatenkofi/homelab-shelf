## Bridge Forward 

Bridge forward is a process that takes place when a packet is forwarded from one bridge port to another, essentially connecting multiple devices on the same network. After receiving a packet on the in-interface, the device determines that the in-interface is a bridge port, so it gets passed through the bridging process: 

1.  A packet goes through the bridge NAT dst-nat chain, where MAC destination and priority can be changed, apart from that, a packet can be simply accepted, dropped, or marked; 

2.  Checks whether the use-ip-firewall option is enabled in the bridge settings; 

3.  Run packet through the bridge host table to make a forwarding decision. A packet that ends up being flooded (e.g. broadcast, multicast, unknown unicast traffic), gets multiplied per bridge port and then processed further in the bridge forward chain. When using `vlan-filtering=yes` , packets that are not allowed due to the "/interface bridge vlan" table, will be dropped at this stage. 

4.  A packet goes through the bridge filter forward chain, where priority can be changed or the packet can be simply accepted, dropped, or marked; 

5.  Checks whether the use-ip-firewall option is enabled in the bridge settings; 

6.  A packet goes through the bridge NAT src-nat chain, where MAC source and priority can be changed, apart from that, a packet can be simply accepted, dropped, or marked; 

7.  Checks whether the use-ip-firewall option is enabled in the bridge settings; 

676 

**==> picture [505 x 423] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**
