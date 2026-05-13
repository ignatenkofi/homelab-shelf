## Output 

Or when a packet is originated from the router (routing output): 

1.  The packet is originated from the router itself 

   - a.  the packet goes through the routing table to make a routing decision 

2.  A packet enters the output process 

   - a.  process packet through the Bridge decision; b.  send the packet through connection tracking; 

   - c.  process packet through the Mangle output chain; 

   - d.  process packet through the Filter output chain; 

   - e.  send the packet to routing adjustment ( policy routing) 

3.   The packet enters postrouting process; 

673 

a.  - 

**==> picture [505 x 423] intentionally omitted <==**

**==> picture [505 x 230] intentionally omitted <==**

- b.  - process packet through NATs src-nat chain; c.  - if there is a hotspot undo any modifications made in hotspot-in; 

674 

   - d.  - process packet through queue tree (HTB Global); e.  - process packet through simple queues; 

4.  Check if there is IPsec and then process through IPsec policies; 

**==> picture [505 x 424] intentionally omitted <==**
