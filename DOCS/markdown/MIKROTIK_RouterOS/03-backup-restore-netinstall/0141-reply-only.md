## Reply Only 

If the ARP property is set to reply-only on the interface, then the router only replies to ARP requests. Neighbour MAC addresses will be resolved using /ip arp statically, but there will be no need to add the router's MAC address to other hosts' ARP tables like in cases where ARP is disabled.
