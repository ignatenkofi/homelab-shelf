## Choosing what to send over the tunnel 

If we look at the generated dynamic policies, we see that only traffic with a specific (received by mode config) source address will be sent through the tunnel. But a router in most cases will need to route a specific device or network through the tunnel. In such a case, we can use source NAT to change the source address of packets to match the mode config address. Since the mode config address is dynamic, it is impossible to create a static source NAT rule. In RouterOS it is possible to generate dynamic source NAT rules for mode config clients.
