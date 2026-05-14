## SPT Calculation 

Assume we have the following network. The network consists of 4(four) routers. OSPF costs for outgoing interfaces are shown near the line that represents the link. In order to build the shortest-path tree for router R1, we need to make R1 the root and calculate the smallest cost for each destination. 

**==> picture [505 x 432] intentionally omitted <==**

994 

**==> picture [505 x 432] intentionally omitted <==**

As you can see from the image above multiple shortest paths have been found to the 172.16.1.0 network, allowing load balancing of the traffic to that destination called equal-cost multipath (ECMP). After the shortest-path tree is built, a router starts to build the routing table accordingly. Networks are reached consequently to the cost calculated in the tree. 

Routing table calculation looks quite simple, however, when some of the OSPF extensions are used or OSPF areas are calculated, routing calculation gets more complicated.
