## Routing Information Base 

**==> picture [504 x 83] intentionally omitted <==**

Routing Information Base is a database that lists entries for particular network destinations and their gateways (address of the next device along the path or simply next-hop). One such entry in the routing table is called a route. 

- A hop occurs when a packet is passed from one network segment to another. 

By default, all routes are organized in one "main" routing table. It is possible to make more than one routing table which we will discuss further in this article, but for now, for sake of simplicity, we will consider that there is only one "main" routing table. 

RIB table contains complete routing information, including static routes and policy routing rules configured by the user, routing information learned from dynamic routing protocols (RIP, OSPF, BGP), and information about connected networks. 

Its purpose is not just to store routes, but also to filter routing information to calculate the best route for each destination prefix, to build and update the Forwarding Information Base, and to distribute routes between different routing protocols.
