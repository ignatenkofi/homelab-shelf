## `/routing/ospf/neighbor` 

List of currently active OSPF neighbors. 

**==> picture [516 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
Read-only Property Description<br>address  (IP) An IP address of the OSPF neighbor router<br>adjacency  (time) Elapsed time since adjacency was formed<br>**----- End of picture text -----**<br>


973 

**==> picture [516 x 430] intentionally omitted <==**

**----- Start of picture text -----**<br>
area  (string)<br>bdr  (string) An IP address of the Backup Designated Router<br>comment  (string)<br>db-summaries  (integer)<br>dr  (IP) An IP address of the Designated Router<br>dynamic  (yes | no)<br>inactive  (yes | no)<br>instance  (string)<br>ls-requests  (integer)<br>ls-retransmits  (integer)<br>priority  (integer) Priority configured on the neighbor<br>router-id  (IP) neighbor router's  RouterID<br>state  (down | attempt | init | 2-<br>way | ExStart | Exchange |  Down  - No Hello packets have been received from a neighbor.<br>Loading | full) Attempt  - Applies only to NBMA clouds. The state indicates that no recent information was received from a<br>neighbor.<br>Init  - Hello packet received from the neighbor, but bidirectional communication is not established (Its own<br>RouterID is not listed in the Hello packet).<br>2-way  - This state indicates that bi-directional communication is established. DR and BDR elections occur<br>during this state, routers build adjacencies based on whether the router is DR or BDR, and the link is point-to-<br>point or a virtual link.<br>ExStart  - Routers try to establish the initial sequence number that is used for the packet information exchange.<br>The router with a higher ID becomes the master and starts the exchange.<br>Exchange  - Routers exchange database description (DD) packets.<br>Loading  - In this state actual link state information is exchanged. Link State Request packets are sent to<br>neighbors to request any new LSAs that were found during the Exchange state.<br>Full  - Adjacency is complete, and neighbor routers are fully adjacent. LSA information is synchronized between<br>adjacent routers. Routers achieve the full state with their DR and BDR only, an exception is P2P links.<br>state-changes  (integer) Total count of OSPF state changes since neighbor identification<br>**----- End of picture text -----**<br>
