## Matchers 

Tables below shows all the properties that can be used as a matchers in the firewall rules. 

Matchers are executed in a specific order. 

For IPv4: 

Source MAC Address In/Out interfaces 

657 

In/Out interface lists IP Range Address type Address list TTL DSCP Length TLS IPv4 Options Dst Port Src Port Any Port TCP Options TCP MSS ICMP Codes Ingress Priority Priority Packet Mark Realm (routing table) Hotsopot Connection Mark Connection State Connection NAT State Connection Bytes Connection Limit Connection Rate Ipsec Policy Helper String (content) PSD Layer7 Random Nth PCC Limit Dst Limit Log 

For IPv6: 

- Address type Address list Source MAC Address In/Out interfaces In/Out interface lists Hop Limit DSCP Length TLS IPv6 Header Dst Port Src Port Any Port TCP Options TCP MSS ICMPv6 Codes Ingress Priority Priority Packet Mark Connection Mark Connection State Connection NAT State Connection Bytes Connection Limit Connection Rate Ipsec Policy 

658 

Helper Match String (content) Random Nth PCC Limit Dst Limit Log 

Properties are split in two parts: 

stateless - properties do not require connection tracking to function and can be used in stateless RAW firewall matching. stateful - properties either require connection tracking to function or is available only in stateful firewall config.
