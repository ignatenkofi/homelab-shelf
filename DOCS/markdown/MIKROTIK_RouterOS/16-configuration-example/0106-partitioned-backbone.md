## Partitioned Backbone 

OSPF allows to linking of discontinuous parts of the backbone area using virtual links. This might be required when two separate OSPF networks are merged into one large network. Virtual links can be configured between separate ABRs that touch the backbone area from each side and have a common area. 

The additional area could be created to become a transit area when a common area does not exist, it is illustrated in the image above. 

Virtual Links are not required for non-backbone areas when they get partitioned. OSPF does not actively attempt to repair area partitions, each component simply becomes a separate area, when an area becomes partitioned. The backbone performs routing between the new areas. Some destinations are reachable via intra-area routing, the area partition requires inter-area routing. 

However, to maintain full routing after the partition, an address range has not to be split across multiple components of the area partition. 

1008 

**==> picture [505 x 169] intentionally omitted <==**
