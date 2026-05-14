## Database Synchronization 

Link-state Database synchronization between OSPF routers is very important. Unsynchronized databases may lead to incorrectly calculated routing tables which could cause routing loops or black holes. 

There are two types of database synchronizations: 

initial database synchronization reliable flooding. 

When the connection between two neighbors first comes up, initial database synchronization will happen. OSPF is using explicit database download when neighbor connections first come up. This procedure is called Database exchange . Instead of sending the entire database, the OSPF router sends only its LSA headers in a sequence of OSPF Database Description (DD) packets. The router will send the next DD packet only when the previous packet is acknowledged. When an entire sequence of DD packets has been received, the router knows which LSAs it does not have and which LSAs are more recent. The router then sends Link-State Request (LSR) packets requesting desired LSAs, and the neighbor responds by flooding LSAs in Link-State Update (LSU) packets. After all the updates are received neighbors are said to be fully adjacent . 

999 

Reliable flooding is another database synchronization method. It is used when adjacencies are already established and the OSPF router wants to inform other routers about LSA changes. When the OSPF router receives such Link State Update, it installs a new LSA in the link-state database, sends an acknowledgment packet back to the sender, repackages LSA in new LSU, and sends it out to all interfaces except the one that received the LSA in the first place. 

OSPF determines if LSAs are up to date by comparing sequence numbers. Sequence numbers start with 0×80000001, the larger the number, the more recent the LSA is. A sequence number is incremented each time the record is flooded and the neighbor receiving the update resets the Maximum age timer. LSAs are refreshed every 30 minutes, but without a refresh, LSA remains in the database for the maximum age of 60 minutes. 

Databases are not always synchronized between all OSPF neighbors, OSPF decides whether databases need to be synchronized depending on the network segment, for example, on point-to-point links databases are always synchronized between routers, but on Ethernet networks databases are synchronized between certain neighbor pairs.
