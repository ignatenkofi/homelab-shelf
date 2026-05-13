## Multicast Address 

The most important multicast aspects are: 

traffic is sent to a single address but is processed by multiple hosts; 

- group membership is dynamic, allowing hosts to join and leave the group at any time; 

- in IPv6, Multicast Listener Discovery (MLD) messages are used to determine group membership on a network segment, also known as a link or subnet; 

a host can send traffic to the group's address without belonging to the corresponding group. 

A single IPv6 multicast address identifies each multicast group. Each group's reserved IPv6 address is shared by all host members of the group who listen and receive any IPv6 messages sent to the group's address. 

The multicast address consists of the following parts: 

The first 8 bits in the multicast address are always 1111 1111 (which is FF in hexadecimal format). 

- The flag uses the 9th to 12th bit and shows if this multicast address is predefined (well-known) or not. If it is well-known, all bits are 0s. Scope ID indicates to which scope multicast address belongs, for example, Scope ID=2 is link-local scope. 

- The group ID is used to specify a multicast group. There are predefined group IDs, such as Group ID=1 - all nodes. Therefore, if the multicast address is ff02::1, that means Scope ID=2 and Group ID=1, indicating all nodes in link-local scope. This is analogous to broadcast on IPv4. 

Here is the table of reserved IPV6 addresses for multicast: 

**==> picture [516 x 99] intentionally omitted <==**

**----- Start of picture text -----**<br>
Address Description<br>FF02::1 The all-nodes address is used to reach all nodes on the same link.<br>FF02::2 The all-routers address is used to reach all routers on the same link.<br>FF02::5 The all-Open Shortest Path First (OSPF) router address is used to reach all OSPF routers on the same link.<br>FF02::6 The all-OSPF-designated router's address is used to reach all OSPF-designated routers on the same link.<br>**----- End of picture text -----**<br>


165 

FF02::1: The solicited-node address is used in the address resolution process to resolve the IPv6 address of a link-local node to its link-layer FFXX: address. The last 24 bits (XX:XXXX) of the solicited-node address are the last 24 bits of an IPv6 unicast address. XXXX 

The following table is a partial list of IPv6 multicast addresses that are reserved for IPv6 multicasting and registered with the Internet Assigned Numbers Authority (IANA). For a complete list of assigned addresses read IANA document. 

Multicast addresses can be used to discover nodes in a network. For example, discover all nodes 

```
mrz@bumba:/media/aaa/ver$ ping6 ff02::1%eth0
PING ff02::1%eth0(ff02::1) 56 data bytes
64 bytes from fe80::21a:4dff:fe5d:8e56: icmp_seq=1 ttl=64 time=0.037 ms
64 bytes from fe80::20c:42ff:fe0d:2c38: icmp_seq=1 ttl=64 time=4.03 ms (DUP!)
64 bytes from fe80::20c:42ff:fe28:7945: icmp_seq=1 ttl=64 time=5.59 ms (DUP!)
64 bytes from fe80::20c:42ff:fe49:fce5: icmp_seq=1 ttl=64 time=5.60 ms (DUP!)
64 bytes from fe80::20c:42ff:fe21:f1ec: icmp_seq=1 ttl=64 time=5.88 ms (DUP!)
64 bytes from fe80::20c:42ff:fe72:a1b0: icmp_seq=1 ttl=64 time=6.70 ms (DUP!)
```
