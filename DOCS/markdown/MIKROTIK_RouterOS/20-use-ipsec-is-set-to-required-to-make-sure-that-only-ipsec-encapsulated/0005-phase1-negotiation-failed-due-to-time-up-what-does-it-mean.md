## "phase1 negotiation failed due to time up" what does it mean? 

There are communication problems between the peers. Possible causes include - misconfigured Phase 1 IP addresses; firewall blocking UDP ports 500 and 4500; NAT between peers not properly translating IPsec negotiation packets. This error message can also appear when a local-address parameter is not used properly. More information available here. 

Random packet drops or connections over the tunnel are very slow, enabling packet sniffer/torch fixes the problem? 

Problem is that before encapsulation packets are sent to Fasttrack/FastPath, thus bypassing IPsec policy checking. The solution is to exclude traffic that needs to be encapsulated/decapsulated from Fasttrack.
