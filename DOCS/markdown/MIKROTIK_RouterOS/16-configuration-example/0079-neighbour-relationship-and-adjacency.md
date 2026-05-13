## Neighbour Relationship and Adjacency 

OSPF is a link-state protocol that assumes that the interface of the router is considered an OSPF link. Whenever OSPF is started, it adds the state of all the links in the local link-state database . 

There are several steps before the OSPF network becomes fully functional: 

- Neighbors discovery Database Synchronization Routing calculation 

Link-state routing protocols are distributing and replicating database that describes the routing topology. The link-state protocol's flooding algorithm ensures that each router has an identical link-state database and the routing table is calculated based on this database. 

After all the steps above are completed link-state database on each neighbor contains full routing domain topology (how many other routers are in the network, how many interfaces routers have, what networks link between router connects, cost of each link, and so on).
