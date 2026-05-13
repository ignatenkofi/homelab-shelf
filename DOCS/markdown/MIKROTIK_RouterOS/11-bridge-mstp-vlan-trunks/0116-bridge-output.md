## Bridge Output 

Bridge output is a process that takes place when a packet should exit the device through one or multiple bridge ports. Most commonly this happens when a bridge interface itself tries to reach a device connected to a certain bridge port (e.g. when a DHCP server running on a bridge interface is responding to a DHCP client). After a packet is processed on other higher-level RouterOS processes and the device finally determines that the output interface is a bridge, the packet gets passed through the bridging process: 

678 

1.  Run packet through the bridge host table to make a forwarding decision. A packet that ends up being flooded (e.g. broadcast, multicast, unknown unicast traffic), gets multiplied per bridge port and then processed further in the bridge output chain. 

2.  A packet goes through the bridge filter output chain, where priority can be changed or the packet can be simply accepted, dropped, or marked; 

3.  A packet goes through the bridge NAT src-nat chain, where MAC source and priority can be changed, apart from that, a packet can be simply accepted, dropped, or marked; 

4.  Checks whether the use-ip-firewall option is enabled in the bridge settings; 

**==> picture [505 x 423] intentionally omitted <==**
