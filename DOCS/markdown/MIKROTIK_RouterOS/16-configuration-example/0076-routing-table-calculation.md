## Routing Table Calculation 

Link state database describes the routers and links that interconnect them and are appropriate for forwarding. It also contains the cost (metric) of each link. This metric is used to calculate the shortest path to the destination network. 

Each router can advertise a different cost for the router's own link direction, making it possible to have asymmetric links (packets to the destination travel over one path, but the response travels a different path). Asymmetric paths are not very popular, because it makes it harder to find routing problems. The value of the cost can be changed in the OSPF interface template configuration menu, for example, to add an ether2 interface with a cost of 100: 

993 

```
/routing ospf interface-template
add interfaces=ether2 cost=100 area=backbone_v2
```

The cost of an interface on Cisco routers is inversely proportional to the bandwidth of that interface. A higher bandwidth indicates a lower cost. If similar costs are necessary on RouterOS, then use the following formula: 

Cost = 100000000/bw in bps. 

OSPF router is using Dijkstra's Shortest Path First (SPF) algorithm to calculate the shortest path. The algorithm places the router at the root of a tree and calculates the shortest path to each destination based on the cumulative cost required to reach the destination. Each router calculates its own tree even though all routers are using the same link-state database.
