## Synchronization on Broadcast Subnets 

On the broadcast segment, there are n*(n-1)/2 neighbor relations, it will be a huge amount of Link State Updates and Acknowledgements sent over the subnet if the OSPF router will try to synchronize with each OSPF router on the subnet. 

**==> picture [505 x 342] intentionally omitted <==**

This problem is solved by electing one Designated Router and one Backup Designated Router for each broadcast subnet. All other routers are synchronizing and forming adjacencies only with those two elected routers. This approach reduces the number of adjacencies from n*(n-1)/2 to only 2n-3. 

The image on the right illustrates adjacency formations on broadcast subnets. Routers R1 and R2 are Designated Routers and Backup Designated routers respectively. For example, if R3 wants to flood Link State Update (LSU) to both R1 and R2, a router sends LSU to the IP multicast address AllDRouters (224.0.0.6) and only DR and BDR listen to this multicast address. Then Designated Router sends LSU addressed to AllSPFRouters, updating the rest of the routers.
