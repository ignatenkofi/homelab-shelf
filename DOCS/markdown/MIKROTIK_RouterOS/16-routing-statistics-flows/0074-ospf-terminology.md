## OSPF Terminology 

Before we move on let's familiarise ourselves with terms important for understanding the operation of the OSPF. These terms will be used throughout the article. 

Neighbor - connected (adjacent) router that is running OSPF with the adjacent interface assigned to the same area. Neighbors are found by Hello packets (unless manually configured). 

- Adjacency - logical connection between a router and its corresponding DR and BDR. No routing information is exchanged unless adjacencies are formed. 

Link - link refers to a network or router interface assigned to any given network. 

- Interface - physical interface on the router. The interface is considered a link when it is added to OSPF. Used to build link database. 

- LSA - Link State Advertisement, data packet contains link-state and routing information, that is shared among OSPF Neighbors. 

- DR - Designated Router, chosen router to minimize the number of adjacencies formed. The option is used in broadcast networks. BDR -Backup Designated Router, hot standby for the DR. BDR receives all routing updates from adjacent routers, but it does not flood LSA updates. 

- Area - areas are used to establish a hierarchical network. 

- ABR - Area Border Router, router connected to multiple areas. ABRs are responsible for summarization and update suppression between 

- connected areas. 

- ASBR - Autonomous System Boundary Router, router connected to an external network (in a different AS). If you import other protocol routes into OSPF from the router it is now considered ASBR. 

- NBMA - Non-broadcast multi-access, networks allow multi-access but have no broadcast capability. Additional OSPF neighbor configuration is required for those networks. 

Broadcast - Network that allows broadcasting, for example, Ethernet. 

Point-to-point - Network type eliminates the need for DRs and BDRs 

- Router-ID - IP address used to identify the OSPF router. If the OSPF Router-ID is not configured manually, a router uses one of the IP addresses assigned to the router as its Router-ID. 

- Link State - The term link-state refers to the status of a link between two routers. It defines the relationship between a router's interface and its neighboring routers. 

Cost - Link-state protocols assign a value to each link called cost. the cost value depends on the speed of the media. A cost is associated with the outside of each router interface. This is referred to as interface output cost. 

Autonomous System - An autonomous system is a group of routers that use a common routing protocol to exchange routing information.
