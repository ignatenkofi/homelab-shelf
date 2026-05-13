## NAT and Fasttrack Bypass 

At this point if you try to send traffic over the IPsec tunnel, it will not work, packets will be lost. This is because both routers have NAT rules (masquerade) that are changing source addresses before a packet is encrypted. A router is unable to encrypt the packet because the source address does not match the address specified in the policy configuration. For more information see the IPsec packet flow example. 

To fix this we need to set up IP/Firewall/NAT bypass rule.
