## Nexthop Lookup 

Nexthop lookup is a part of the route selection process. Its main purpose is to find a directly reachable gateway address (next-hop). Only after a valid next-hop is selected router knows which interface to use for packet forwarding. 

Nexthop lookup becomes more complicated if routes have a gateway address that is several hops away from this router (e. g. iBGP, multihop eBGP). Such routes are installed in the FIB after the next-hop selection algorithm determines the address of the directly reachable gateway (immediate next-hop). 

It is necessary to restrict the set of routes that can be used to look up immediate next-hops. Nexthop values of RIP or OSPF routes, for example, are supposed to be directly reachable and should be looked up only using connected routes. This is achieved using scope and target-scope properties. 

Routes with a scope greater than the maximum accepted value are not used for next-hop lookup. Each route specifies the maximum accepted scope value for its nexthop in the target- 

**==> picture [293 x 248] intentionally omitted <==**

scope property. The default value of this property allows nexthop lookup only through connected routes, with the exception of iBGP routes that have a larger default value and can lookup nexthop also through IGP and static routes. 

There are changes in RouterOS v7 nexthop lookup. 

Routes are processed in scope order, and updates to routes with a larger scope cannot affect the state of nexthop lookup for routes with a smaller scope. 

Consider an example from v6: 

183 

```
/ip route add dst-address=10.0.1.0/24 gateway=10.0.0.1
    scope=50 target-scope=30 comment=A
/ip route add dst-address=10.0.2.0/24 gateway=10.0.0.1
    scope=30 target-scope=20 comment=B
/ip route add dst-address=10.0.0.0/24 scope=20 gateway=WHATEVER
    comment=C
```

Gateway 10.0.0.1 is recursively resolved through C using the smallest referring scope (scope 20 from route B), both routes are active. Now we change both A and B at the same time: 

```
/ip route set A target-scope=10
```

Suddenly, applying an update to route A makes the gateway of route B inactive. This is because in v6 there is only one gateway object per address. 

v7 keeps multiple gateway objects per address, one for each combination of scope and gateway check. 

When `target-scope` or gateway check of a route is changed, ROS v7 will not affect other routes , as it does in v6. In v7 target-scope and gateway check are properties that are internally attached to the gateway, not to the route. 

Scope values considered as invalid and fixed automatically: 

if gateway scope is set to 255 - RouterOS will internally fix this error by setting gateway scope to 254. 

if route scope is less than gateway scope - RouterOS will internally fix this error by setting route scope to "gateway scope + 1" 

Used actual scope and target scope values can be seen in `/routing/nexthop` menu 

Gateway check can be extended by setting `check-gateway` parameter. Gateway reachability can be checked by sending ARP probes, or ICMP messages or by checking active BFD sessions. The router periodically (every 10 seconds) checks the gateway by sending either an ICMP echo request (pi ng) or an ARP request (arp). If no response from the gateway is received for 10 seconds, the request times out. After two timeouts gateway is considered unreachable. After receiving a reply from the gateway it is considered reachable and the timeout counter is reset.
