## Ethernet 

The most commonly used link layer protocol (OSI Layer2) in computer networks is the Ethernet protocol. In order to communicate, each node has a unique assigned address, called MAC (Media Access Control address) sometimes it is also called an Ethernet address. 

It is 48-bit long and typically fixed by the manufacturer (cannot be changed), but in recent years customization of MAC addresses is widely used, RouterOS also allows to set custom MAC address. 

Most commonly used MAC format is 6 hexadecimal numbers separated by colons ( `D4:CA:6D:01:22:96` ) 

RouterOS shows MAC address in a configuration for all Ethernet-like interfaces (Wireless, 60G, VPLS, etc.) 

```
[admin@rack1_b32_CCR1036] /interface ethernet> print
Flags: X - disabled, R - running, S - slave
 #    NAME                  MTU MAC-ADDRESS       ARP             SWITCH
 0 R  ether1               1500 D4:CA:6D:01:22:96 enabled
 1 R  ether2               1500 D4:CA:6D:01:22:97 enabled
 2 R  ether3               1500 D4:CA:6D:01:22:98 enabled
 3    ether4               1500 D4:CA:6D:01:22:99 enabled
 4    ether5               1500 D4:CA:6D:01:22:9A enabled
 5    ether6               1500 D4:CA:6D:01:22:9B enabled
 6    ether7               1500 D4:CA:6D:01:22:9C enabled
 7 R  ether8               1500 D4:CA:6D:01:22:9D enabled
 8    sfp-sfpplus1         1500 D4:CA:6D:01:22:94 enabled
 9    sfp-sfpplus2         1500 D4:CA:6D:01:22:95 enabled
```

There are three types of addresses: 

151 

**==> picture [406 x 148] intentionally omitted <==**

Unicast address is sent to all nodes within the collision domain, which typically is Ethernet cable between two nodes or in case of wireless all receivers that can detect wireless signals. Only remote node with matching MAC address will accept the frame (unless the promiscuous mode is enabled) 

One of the special addresses is broadcast address ( `FF:FF:FF:FF:FF:FF` ), a broadcast frame is accepted and forwarded over Layer2 network by all nodes Another special address is multicast . Frames with multicast addresses are received by all nodes configured to receive frames with this address.
