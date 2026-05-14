## Reactive mode 

1496 

**==> picture [390 x 236] intentionally omitted <==**

Router A wants to discover a path to C 

**==> picture [390 x 237] intentionally omitted <==**

Router C sends a unicast response to A 

In reactive mode, HWMP+ is very much like AODV (Ad-hoc On-demand Distance Vector). All paths are discovered on-demand, by flooding Path Request (PREQ) message in the network. The destination node or some router that has a path to the destination will reply with a Path Response (PREP). Note that if the destination address belongs to a client, the AP this client is connected to will serve as a proxy for him (i.e. reply to PREQs on his behalf). 

This mode is best suited for mobile networks, and/or when most of the communication happens between intra-mesh nodes.
