## Partial offloading 

In the case of DX3000/DX2000 switch chip serries, it is quite simple: one RouterOS route entry (/ip/route/) reflects into one HW IPv4 route prefix entry. Connected hosts (/32 routes) also occupy the same table. As long as the total number of routes ("ip/route print count-only") + connected host count ("/ip /arp print count-only where status=reachable or status=stale") , 13312 (13k) , everything gets offloaded. Exceeding the number, routes with shorter prefixes stay on the CPU.
