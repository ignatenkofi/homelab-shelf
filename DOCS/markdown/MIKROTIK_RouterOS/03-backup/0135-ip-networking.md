## IP Networking 

Ethernet protocol is sufficient to get data between two nodes on an Ethernet network, but it is not used on its own. For Internet/Networking layer (OSI Layer 3) IP (Internet Protocol) is used to identify hosts with unique logical addresses. 

Most of the current networks use IPv4 addresses, which are 32bit address written in dotted-decimal notation ( `192.168.88.1` ) 

There can be multiple logical networks and to identify which network IP address belongs to, the netmask is used. Netmask typically is specified as a number of bits used to identify a logical network. The format can also be in decimal notation, for example, the 24-bit netmask can be written as `255.25 5.255.0` 

Let's take a closer look at 192.168.3.24/24: 

```
11000000 10101000 00000011 00011000 => 192.168.3.24
11111111 11111111 11111111 00000000 => /24 or 255.255.255.0
```

As can be seen from the illustration above high 24 bits are masked, leaving us with a range of 0-255. 

From this range, the first address is used to identify the network (in our example network address would be 192.168.3.0) and the last one is used for network broadcast (192.168.3.255). That leaves us with a range from 1 to 254 for host identification which is called unicast addresses. 

The same as in Ethernet protocol there can be also special addresses: 

broadcast - address to send data to all possible destinations ("all-hosts broadcast"), which permits the sender to send the data only once, and all receivers receive a copy of it. In the IPv4 protocol, the address 255.255.255.255 is used for local broadcast. In addition, a directed (limited) broadcast can be made to network broadcast address; 

multicast - address associated with a group of interested receivers. In IPv4, addresses `224.0.0.0` through `239.255.255.255` are designated as multicast addresses. The sender sends a single datagram from its unicast address to the multicast group address and the intermediary routers take care of making copies and sending them to all receivers that have joined the corresponding multicast group; 

In case of logical IP network, unicast, broadcast and multicast visualization would look a bit different 

152 

**==> picture [406 x 148] intentionally omitted <==**

There are also address ranges reserved for a special purpose, for example, private address range, that should be used only in local networks and typically are dropped when forwarded to the internet: 

10.0.0.0/8 - start: 10.0.0.0; end: 10.255.255.255 172.16.0.0/12 - start: 172.16.0.0; end:172.31.255.255 192.168.0.0/16 - start: 192.168.0.0; end: 192.168.255.255
