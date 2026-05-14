## Understanding OSPF Areas 

A distinctive feature of OSPF is the possibility to divide AS into multiple routing Areas which contain their own set of neighbors. Imagine a large network with 300+ routers and multiple links between them. Whenever link flaps or some other topology change happens in the network, this change will be flooded to all OSPF devices in the network resulting in a quite heavy load on the network and even downtime since network convergence may take some time for such a large network. 

A large single-area network can produce serious issues: 

- Each router recalculates the database every time whenever network topology change occurs, the process takes CPU resources. 

- Each router holds an entire link-state database, which shows the topology of the entire network, it takes memory resources. 

- A complete copy of the routing table and a number of routing table entries may be significantly greater than the number of networks, which can take even more memory resources. 

- Updating large databases requires more bandwidth. 

The introduction of areas allows for better resource management since topology change inside one area is not flooded to other areas in the network. The concept of areas enables simplicity in network administration as well as routing summarization between areas significantly reducing the database size that needs to be stored on each OSPF neighbor. This means that each area has its own link-state database and corresponding shortest-path tree. 

The structure of an area is invisible to other areas. This isolation of knowledge makes the protocol more scalable if multiple areas are used; routing table calculation takes fewer CPU resources and routing traffic is reduced. 

However, multi-area setups create additional complexity. It is not recommended to separate areas with fewer than 50 routers. The maximum number of routers in one area is mostly dependent on the CPU power you have for routing table calculation. 

**==> picture [505 x 153] intentionally omitted <==**

1001 

OSPF area has unique 32-bit identification (Area ID) and the area with an Area ID of 0.0.0.0 (called the Backbone area) is the main one where any other area should connect. Routers that connect to more than one area are called ABR (Area Border Routers), and their main responsibility is summarization and update suppression between connected areas. The router connecting to another routing domain is called ASBR (Autonomous System Boundary Router). 

Each area has its own link-state database, consisting of router-LSAs and network-LSAs describing how all routers within that area are interconnected. Detailed knowledge of the area's topology is hidden from all other areas; router-LSAs and network-LSAs are not flooded beyond the area's borders. Area Border Routers ( ABR s) leak addressing information from one area into another in OSPF summary-LSAs. This allows one to pick the best area border router when forwarding data to destinations from another area and is called intra-area routing . 

Routing information exchange between areas is essentially a Distance Vector algorithm and to prevent algorithm convergence problems, such as counting to infinity, all areas are required to attach directly to the backbone area making a simple hub-and-spoke topology. The area-ID of the backbone area is always 0.0.0.0 and can not be changed. 

RouterOS area configuration is done in the `/routing/ospf/area` menu.  For example, a configuration of an ABR router with multiple attached areas, one Stub area, and one default area:
