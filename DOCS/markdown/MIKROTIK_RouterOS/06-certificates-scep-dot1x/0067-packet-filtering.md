## Packet Filtering 

From /ip firewall filter print dynamic command, you can get something like this (comments follow after each of the rules): 

```
 0 D chain=forward action=jump jump-target=hs-unauth hotspot=from-client,!auth
```

Any packet that traverse the router from an unauthorized client will be sent to the hs-unauth chain. The hs-unauth implements the IP-based Walled Garden filter. 

```
 1 D chain=forward action=jump jump-target=hs-unauth-to hotspot=to-client,!auth
```

Everything that comes to clients through the router, gets redirected to another chain, called hs-unauth-to . This chain should reject unauthorized requests to the clients. 

```
 2 D chain=input action=jump jump-target=hs-input hotspot=from-client
```

Everything that comes from clients to the router itself, gets to yet another chain, called hs-input 

. 

```
 3 I chain=hs-input action=jump jump-target=pre-hs-input
```

Before proceeding with [predefined] dynamic rules, the packet gets to the administratively controlled pre-hs-input chain, which is empty by default, hence the invalid state of the jump rule. 

- `4 D chain=hs-input action=accept dst-port=64872 protocol=udp` 

- `5 D chain=hs-input action=accept dst-port=64872-64875 protocol=tcp` 

Allow client access to the local authentication and proxy services (as described earlier). 

```
 6 D chain=hs-input action=jump jump-target=hs-unauth hotspot=!auth
```

All other traffic from unauthorized clients to the router itself will be treated the same way as the traffic traversing the routers. 

- `7 D chain=hs-unauth action=return protocol=icmp` 

- `8 D ;;; www.mikrotik.com` 

```
     chain=hs-unauth action=return dst-address=66.228.113.26 dst-port=80 protocol=tcp
```

305 

Unlike the NAT table where only TCP-protocol related Walled Garden entries were added, in the packet filter hs-unauth chain is added to everything you have set in the /ip hotspot walled-garden ip menu. That is why although you have seen only one entry in the NAT table, there are two rules here. 

```
 9 D chain=hs-unauth action=reject reject-with=tcp-reset protocol=tcp
```

```
10 D chain=hs-unauth action=reject reject-with=icmp-net-prohibited
```

Everything else that has not been white-listed by the Walled Garden will be rejected. Note the usage of TCP Reset for rejecting TCP connections. 

```
11 D chain=hs-unauth-to action=return protocol=icmp
12 D ;;; www.mikrotik.com
     chain=hs-unauth-to action=return src-address=66.228.113.26 src-port=80 protocol=tcp
```

The same action as in rules #7 and #8 is performed for the packets destined to the clients (chain hs-unauth-to ) as well. 

```
13 D chain=hs-unauth-to action=reject reject-with=icmp-host-prohibited
```

Reject all packets to the clients with an ICMP reject message. 

306
