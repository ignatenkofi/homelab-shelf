## Logical Interfaces 

So far we looked at examples when in or out interfaces are actual physical interfaces (Ethernet, wireless), but how packets will flow if the router receives tunnel encapsulated packets? 

**==> picture [504 x 233] intentionally omitted <==**

Let's assume that there is an IPIP packet coming into the router. Since it is a regular ipv4 packet it will be processed through all routing-related facilities ( until "J" in the diagram). Then the router will look if the packet needs to be decapsulated., in this case, it is an IPIP packet so "yes" send the packet to decapsulation. After that packet will go another loop through all the facilities but this time as a decapsulated IPv4 packet. 

It is very important because the packet actually travels through the firewall twice, so if there is a strict firewall, then there should be "accept" rules for IPIP encapsulated packets as well as decapsulated IP packets. 

**==> picture [13 x 13] intentionally omitted <==**

Packet encapsulation and decapsulation using a bridge with enabled `vlan-filtering` do not relate to logical interfaces. See more details in the bridging section.
