## Connection states 

Based on connection table entries arrived packet can get assigned one of the connection states: new, invalid, established, related, or untracked . 

630 

There are two different methods when the packet is considered new . The first one is in the case of stateless connections (like UDP) when there is no connection entry in the connection table. The other one is in the case of a stateful protocol (TCP). In this case, a new packet that starts a new connection is always a TCP packet with an SYN flag. 

If a packet is not new it can belong to either an established or related connection or not belong to any connection making it invalid . A packet with an establis hed state, as most of you already guessed, belongs to an existing connection from the connection tracking table. A related state is very similar, except that the packet belongs to a connection that is related to one of the existing connections, for example, ICMP error packets or FTP data connection packets. 

Connection state notrack is a special case when RAW firewall rules are used to exclude connection from connection tracking. This rule would make all forwarded traffic bypass the connection tracking, improving packet processing speed through the device. 

Any other packet is considered invalid and in most cases should be dropped. 

Based on this information we can set a basic set of filter rules to speed up packet filtering and reduce the load on the CPU by accepting established/related packets, dropping invalid packets, and working on more detailed filtering only for new packets.
