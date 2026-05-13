## RAW Filtering 

The firewall RAW table allows to selectively bypass or drop packets before connection tracking, that way significantly reducing the load on the CPU. The tool is very useful for DoS/DDoS attack mitigation. 

RAW filter configuration is accessible from `ip/firewall/raw` menu for IPv4 and `ipv6/firewall/raw` menu for IPv6. The RAW table does not have matchers that depend on connection tracking ( like connection-state, layer7, etc.). If a packet is marked to bypass the connection tracking packet de-fragmentation will not occur. 

Also RAW firewall can have rules only in two chains: 

642 

prerouting - used to process any packet entering the router 

output - used to process packets originated from the router and leaving it through one of the interfaces. Packets passing through the router are not processed against the rules of the output chain 

And has one specific action: 

Property Description action (action name; Default: accept ) `notrack` - do not send a packet to connection tracking. Useful when you still need to use regular firewall, but do not require connection tracking.
