## Routing table lookup 

**==> picture [505 x 467] intentionally omitted <==**

FIB uses the following information from the packet to determine its destination: 

source address destination address source interface routing mark 

Possible routing decisions are: 

receive packet locally discard the packet (either silently or by sending an ICMP message to the sender of the packet) 

186 

send the packet to a specific IP address on a specific interface 

Run routing decision: 

check that the packet has to be locally delivered (the destination address is the address of the router) process implicit policy routing rules 

process policy routing rules added by a user 

process implicit catch-all rule that looks up the destination in the ''main'' routing table the returned result is "network unreachable" 

The result of the routing decision can be: 

IP address of nexthop + interface 

point-to-point interface local delivery discard ICMP prohibited ICMP host unreachable ICMP network unreachable 

Rules that do not match the current packet are ignored. If a rule has action: 

drop or unreachable , then it is returned as a result of the routing decision process. 

lookup then the destination address of the packet is looked up in the routing table that is specified in the rule. If the lookup fails (no route matches the destination address of the packet), then FIB proceeds to the next rule. 

lookup-only is similar to lookup except that lookup fails if none of the routes in the table matches the packet. 

Otherwise: 

if the type of the route is blackhole  prohibit, , or unreachable, then return this action as the routing decision result; if this is a connected route or route with an interface as the gateway value, then return this interface and the destination address of the packet as the routing decision result; 

if this route has an IP address as the value of the gateway , then return this address and associated interface as the routing decision result; if this route has multiple values of nexthop, then pick one of them in a round-robin fashion. 

Keep in mind that setting interface as a gateway for static routes in general is not a good idea. Interface gateway is useful only in tow scenarios: 

- on point to point type interfaces 

on interfaces where dst address is directly connected, 

as already stated above if interface is set as a gateway routing decision return interface and the destination address of the packet as the result, which menas that, on a broadcast network router will try to resolve packets destination address over the interface by sending ARP probes. If none of the hosts in the same broadcast domain has the IP address, forwarding will fail. So such gateways cannot be used to route packets which destination is multiple hops away. 

**==> picture [13 x 13] intentionally omitted <==**

`gateway` set as non point-to-point interface cannot be used to forward packets with destination multiple hops away. 

Also it is not possible to use `check-gateway` parameter on such gateways for obvious reasons, there is no known destination IP.
