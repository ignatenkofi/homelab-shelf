## Election process 

To properly configure STP in your network you need to understand the election process and which parameters are involved in which order. In RouterOS, the root bridge will be elected based on the smallest priority and the smallest MAC address in this particular order: 

1.  Bridge priority (lowest) 

2.  Bridge MAC address (lowest) 

In RouterOS root ports are elected based on the lowest Root port path cost, lowest bridge identifier, and lowest bridge port ID in this particular order: 

1.  Root port path cost (lowest) 

2.  Bridge identifier (lowest) 3.  Bridge port ID (lowest) 

First, when the device considers which of its ports to elect as the root port, it will check the root path cost seen by its ports. If the root path cost is the same for two or more ports then the Bridge identifier of the upstream device will be checked and the port connected to the lowest bridge identifier will become the root port. If the same bridge identifier is seen on two or more ports, then the Bridge port ID of the upstream device will be checked.
