## Q. How is this better than OSPF/RIP/layer-3 routing in general? 

A. WDS networks usually are bridged, not routed. The ability to self-configure is important for mesh networks, and routing generally requires much more configuration than bridging. Of course, you can always run any L3 routing protocol over a bridged network, but for mesh networks that usually makes little sense. 

1499 

**==> picture [13 x 13] intentionally omitted <==**

Since optimized layer-2 multicast forwarding is not included in the mesh protocol, it is better to avoid forwarding any multicast traffic (including OSPF) over meshed networks. If you need OSPF, then you have to configure OSPF NBMA neighbors that use unicast mode instead.
