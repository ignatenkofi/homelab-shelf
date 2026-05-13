## Input 

We already learned that packet goes into the in-interface, the router determines that it is an IP packet and needs to be routed, and here starts the complicated process: 

1.  A very similar process happens when a packet's destination is a router (routing input): Packet enters prerouting processing: 

   - a.  - check if there is a hotspot and modify the packet for hotspot use; 

   - b.  - process packet through RAW prerouting chain; c.  - send a packet through connection tracking; d.  - process packet through Mangle prerouting chain; 

   - e.  - process packet through NATs dst-nat chain; 

2.  Run packet through routing table to make routing decision; 

3.  A Packet enters the input process; 

   - a.  - process packet through Mangle input chain; 

   - b.  - process packet through Filter input chain; 

   - c.  - process packet through queue tree (HTB Global); 

   - d.  - process packet through simple queues; 

4.  Check if there is IPsec and then process through IPsec policies.
