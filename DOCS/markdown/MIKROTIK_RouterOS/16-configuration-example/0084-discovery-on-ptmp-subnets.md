## Discovery on PTMP Subnets 

Point-to-MultiPoint treats the network as a collection of point-to-point links. 

By design, PTMP networks should not have broadcast capabilities, which means that OSPF neighbors (the same way as for NBMA networks) must be discovered initially through configuration and all communication happens by sending unicast packets directly between neighbors. On RouterOS static neighbor configuration is set in the `/routing ospf static-neighbor` menu. Designated Routers and Backup Designated Routers are not elected on Point-to-multipoint subnets. 

For PTMP networks that do support broadcast, a hybrid type named "ptmp-broadcast" can be used. This network type uses multicast Hellos to discover neighbors automatically and detect bidirectional communication between neighbors. After neighbor detection "ptmp-broacast" sends unicast packets directly to the discovered neighbors. This mode is compatible with the RouterOS v6 "ptmp" type.
