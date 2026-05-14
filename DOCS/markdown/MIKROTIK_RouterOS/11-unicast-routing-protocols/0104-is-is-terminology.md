## IS-IS Terminology 

- IS - Intermediate System is a router capable of forwarding traffic between distantly located hosts. 

- LSP - Link State PDU contains information on the router's local state (usable interfaces, reachable neighbours, and the cost of the interfaces) SPF - Shortest-path-first algorithm 

- DIS - designated intermediate system. DIS ensures that all routes in the network maintain synchronised database. Separate DISs are elected for L1 and L2 routing. Election of the DIS is based on the highest interface priority. Level-1 (L1) routing - Controls distribution of routing information within an IS-IS area. L1 routing is based on system ID. Level-2 (L2) routing - Controls distribution of routing information between IS-IS areas. L2 routing is based on area ID. 

- IS-IS Adjacency - link between IS-IS neighbours. The type of adjacency formed depends on the parameters exchanged in the IS-IS Hello packets. Each of the the adjacent routers runs the DIS election process to determine whether it is eligible to be an L1 or L2 DIS on the broadcast network.
