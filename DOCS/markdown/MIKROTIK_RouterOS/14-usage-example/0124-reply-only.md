## Reply Only 

If ARP property is set to `reply-only` on the interface, then the router only replies to ARP requests. Neighbor MAC addresses will be resolved only using statically configured entries from the " `/ip arp` " menu, but there will be no need to add the router's MAC address to other hosts' ARP tables like in case if ARP is disabled.
