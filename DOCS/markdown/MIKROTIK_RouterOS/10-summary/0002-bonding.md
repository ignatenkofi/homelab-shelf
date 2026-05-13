## Bonding 

573 

Bonding interfaces are used when a larger amount of bandwidth is required, this is done by creating a link aggregation group, which also provides hardware automatic failover and load balancing for switches. By adding two 10Gbps interfaces to bonding, you can increase the theoretical bandwidth limit to 20Gbps. Make sure that all bonded interfaces are linked to the same speed rates. 

**==> picture [13 x 13] intentionally omitted <==**

When using the hardware-offloaded bridge, the CRS3xx, CRS5xx, CCR2116, and CCR2216 devices aggregate traffic using the built-in switch chip without using CPU resources. To route the traffic a router with a powerful CPU is required to handle the aggregated traffic. 

To create a 20Gbps bonding interface from sfp-sfpplus1 and sfp-sfpplus2 between SwitchA to SwitchB and between SwitchC to SwitchB, use these commands on SwitchA and SwitchC :
