## Forwarding Address 

OSPF router can set the forwarding-address to something other than itself which indicates that an alternate next-hop is possible. Mostly forwarding address is set to 0.0.0.0 suggesting that the route is reachable only via the advertising router. 

The forwarding address is set in LSA if the following conditions are met: 

OSPF must be enabled on the next-hop interface 

Next-hop address falls into the network provided by OSPF networks 

A router that receives such LSA can use a forwarding address if OSPF is able to resolve the forwarding address. If forwarding address is not resolved directly - router sets nexthop for forwading address from LSA as a gateway, if forwarding address is not resolved at all - the gateway will be originator-id. Resolve happens only using OSPF instance routes, not the whole routing table. 

Let's look at the example setup below: 

995 

**==> picture [464 x 211] intentionally omitted <==**

Router R1 has a static route to the external network 192.168.0.0/24. OSPF is running between R1, R2, and R3, and the static route is distributed across the OSPF network. 

The problem in such a setup is obvious, R2 can not reach the external network directly. Traffic going to the LAN network from R2 will be forwarded over the router R1 , but if we look at the network diagram we can see that more R2 can directly reach the router where the LAN network i located. 

So knowing the forwarding address conditions, we can make router R1 to set the forwarding address. We simply need to add 10.1.101.0/24 network to OSPF networks in the router's R1 configuration: 

```
/routing/ospf/interface-template add area=backbone_v2 networks=10.1.101.0/24
```

Now lets verify that forwarding address is actually working: 

```
[admin@r2] /ip/route> print where dst-address=192.168.0.0/24
Flags: D - DYNAMIC; A - ACTIVE; o, y - COPY
Columns: DST-ADDRESS, GATEWAY, DISTANCE
    DST-ADDRESS       GATEWAY            DISTANCE
DAo 192.168.0.0/24    10.1.101.1%ether1       110
```

On all OSPF routers you will see LSA set with forwarding address other than 0.0.0.0 

```
[admin@r2] /routing/ospf/lsa> print where id=192.168.0.0
Flags: S - self-originated, F - flushing, W - wraparound; D - dynamic
 1  D instance=default_ip4 type="external" originator=10.1.101.10 id=192.168.0.0
      sequence=0x80000001 age=19 checksum=0xF336 body=
        options=E
        netmask=255.255.255.0
        forwarding-address=10.1.101.1
        metric=10 type-1
        route-tag=0
```

**==> picture [13 x 13] intentionally omitted <==**

OSPF adjacency between routers in the 10.1.101.0/24 network is not required 

996
