## Traffic Storm Control 

Since RouterOS v6.42 it is possible to enable traffic storm control. A traffic storm can emerge when certain frames are continuously flooded on the network. Storm control settings is generally configured on non-uplink ports to restrict incoming storm traffic on those specific ports. This helps safeguard the entire switch and its connected ports by minimizing the impact of traffic storms across the network. 

For example, if a network loop has been created and no loop avoidance mechanisms are used (e.g. Spanning Tree Protocol), broadcast or multicast frames can quickly overwhelm the network, causing degraded network performance or even complete network breakdown. With CRS3xx, CRS5xx series switches and CCR2116, CCR2216 routers it is possible to limit broadcast, unknown multicast and unknown unicast traffic. Unknown unicast traffic is considered when a switch does not contain a host entry for the destined MAC address. Unknown multicast traffic is considered when a switch does not contain a multicast group entry in the `/interface bridge mdb` menu. Storm control settings should be applied to ingress ports, the egress traffic will be limited. 

404 

**==> picture [505 x 216] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

The storm control parameter is specified in percentage (%) of the link speed. If your link speed is 1Gbps, then specifying `storm-rate` as `10` will allow only 100Mbps of broadcast, unknown multicast and/or unknown unicast traffic to be forwarded.
