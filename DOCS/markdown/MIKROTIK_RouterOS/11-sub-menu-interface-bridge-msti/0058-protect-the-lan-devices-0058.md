## Protect the LAN devices 

This step is more important than it is for IPv4. In IPv4 setups clients mostly have addresses from local address range and are NATed to public IP, that way they are not directly reachable from the public networks. 

IPv6 is a different story. In most common setups, enabled IPv6 makes your clients available from the public networks, so proper firewall filter rules to protect your customers are mandatory. 

In brief we will very basic LAN protection should: 

accept established/related and work with new packets; drop invalid packets; 

accept ICMPv6 packets; 

accept new connections originated only from your clients to the public network; drop everything else.
