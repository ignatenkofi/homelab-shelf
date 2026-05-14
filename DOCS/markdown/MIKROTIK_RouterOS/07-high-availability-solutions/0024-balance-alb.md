## balance-alb 

767 

The mode is basically the same as balance-tlb but incoming IPv4 traffic is also balanced. The receive load balancing is achieved by ARP negotiation. The bonding driver intercepts locally generated ARP messages on their way out and overwrites the source hardware address with the unique address of one of the slaves in the bond such that different peers use different hardware addresses. Only MII link monitoring is supported (ARP link monitoring is ignored when configured), the additional downside of this mode is that it requires device driver capability to change MAC address. The mode is not compatible with l ocal-proxy-arp setting. 

**==> picture [481 x 301] intentionally omitted <==**

The image above illustrates how balance-alb mode works. Compared to balance-tlb mode, traffic from clients can also use the secondary link to communicate with the router.
