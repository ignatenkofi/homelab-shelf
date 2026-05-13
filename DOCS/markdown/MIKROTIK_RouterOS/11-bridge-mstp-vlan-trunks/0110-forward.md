## Forward 

Now, let's take our first example where the packet gets routed over the router and look deeper through what facilities packet goes: 

We already learned that packet goes into the in-interface, the router determines that it is an IP packet and needs to be routed, and here starts the complicated process: 

1.   The packet enters prerouting processing: a.  check if there is a hotspot and modify the packet for hotspot use 

   - b.  process packet through RAW prerouting chain; 

   - c.  send the packet through connection tracking; 

   - d.  process packet through Mangle prerouting chain; 

   - e.   process packet through NATs dst-nat chain; 

2.  Run packet through routing table to make routing decision; 3.  The packet enters the forward process; 

671 

   - a.  check TTL value; 

   - b.  process packet through Mangle forward chain; 

   - c.  process packet through the Filter forward chain; 

   - d.  send the packet to accounting processes; 

4.  A packet enters postrouting process; 

   - a.  process packet through Mangle postrouting chain; b.  process packet through NATs src-nat chain; 

   - c.  if there is a hotspot undo any modifications made in hotspot-in; 

   - d.  process packet through queue tree (HTB Global); e.  process packet through simple queues; 

5.  Check if there is IPsec and then process through IPsec policies; 

**==> picture [505 x 423] intentionally omitted <==**

672 

**==> picture [505 x 230] intentionally omitted <==**
