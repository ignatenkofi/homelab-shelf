## Communication Between OSPF Routers 

OSPF operates over the IP network layer using protocol number 89. 

A destination IP address is set to the neighbor's IP address or to one of the OSPF multicast addresses AllSPFRouters (224.0.0.5) or AllDRRouters (224.0.0.6). The use of these addresses is described later in this article. 

Every OSPF packet begins with a standard 24-byte header. 

**==> picture [301 x 123] intentionally omitted <==**

Field Description Packet There are several types of OSPF packets: Hello packet, Database Description (DD) packet, Link state request packet, Link State Update type packet, and Link State Acknowledgement packet. All of these packets except the Hello packet are used in link-state database synchronization. Router one of the router's IP addresses unless configured manually ID Area ID Allows OSPF router to associate the packet to the proper OSPF area. Checksum Allows receiving router to determine if a packet was damaged in transit. Authenti These fields allow the receiving router to verify that the packet's contents were not modified and that packet really came from the OSPF cation router whose Router ID appears in the packet. fields 

There are five different OSPF packet types used to ensure proper LSA flooding over the OSPF network. 

Hello packet - used to discover OSPF neighbors and build adjacencies. 

Database Description (DD) - check for Database synchronization between routers. Exchanged after adjacencies are built. 

- Link-State Request (LSR) - used to request up-to-date pieces of the neighbor's database. Out-of-date parts of the routing database are determined after the DD exchange. 

997 

Link-State Update (LSU) - carries a collection of specifically requested link-state records. 

Link-State Acknowledgment (LSack) - is used to acknowledge other packet types that way introducing reliable communication.
