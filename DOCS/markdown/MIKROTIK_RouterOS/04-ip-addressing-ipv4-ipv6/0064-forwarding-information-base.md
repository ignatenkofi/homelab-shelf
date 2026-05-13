## Forwarding Information Base 

FIB (Forwarding Information Base) contains a copy of the information that is necessary for packet forwarding: 

all active routes policy routing rules 

Each route has dst-address property, that specifies all destination addresses this route can be used for. If several routes apply to a particular IP address, the most specific one (with the largest netmask) is used. This operation (finding the most specific route that matches the given address) is called ''routing table lookup''. 

185 

Only one Best route can be used for packet forwarding. In cases where the routing table contains several routes with the same dst-address , all equally best routes are combined into one ECMP route. The best route is installed into FIB and marked as ''active''. 

When forwarding decision uses additional information, such as the source address of the packet, it is called policy routing . Policy routing is implemented as a list of policy routing rules, that select different routing tables based on the destination address, source address, source interface, and routing mark (which can be changed by firewall mangle rules) of the packet.
