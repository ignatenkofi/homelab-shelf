## Sub-menu: `/interface gre` 

Standards: RFC1701 

GRE (Generic Routing Encapsulation) is a tunneling protocol that was originally developed by Cisco. It can encapsulate a wide variety of protocols creating a virtual point-to-point link. 

GRE is the same as IPIP and EoIP which were originally developed as stateless tunnels. This means that if the remote end of the tunnel goes down, all traffic that was routed over the tunnels will get blackholed. To solve this problem, RouterOS has added a 'keepalive' feature for GRE tunnels. 

**==> picture [13 x 13] intentionally omitted <==**

GRE tunnel adds a 24 byte overhead (4-byte gre header + 20-byte IP header). GRE tunnel can forward only IP and IPv6 packets (ethernet type 800 and 86dd). Do not use the "Check gateway" option "arp" when a GRE tunnel is used as a route gateway.
