## How Routing Works 

Let's look at a basic configuration example to illustrate how routing is used to forward packets between two local networks and to the Internet. 

In this setup, we have several networks: 

two client networks (192.168.2.0/24 and 192.168.1.0/24); 

one network to connect routers (172.16.1.0/30), usually called backbone; 

the last network (10.1.1.0/24) connects our gateway router (Router1) to the internet. 

**==> picture [504 x 164] intentionally omitted <==**

Router 2: 

```
/ip address
add address=172.16.1.2/30 interface=ether1
add address=192.168.2.1/24 interface=bridge2
```

Router1 (gateway) where ether1 connects to the internet: 

178 

```
/ip address
add address=10.1.1.2/24 interface=ether1
add address=172.16.1.1/30 interface=ether2
add address=192.168.1.1/24 interface=bridge1
```

If we look, for example, at the Router1 routing table, we can see that the router knows only about directly connected networks. At this point, when the Client from LAN1 tries to reach the client from LAN2 (192.168.2.0/24), a packet will be dropped on the router, because the destination is unknown for the particular router: 

```
[admin@MikroTik] > /ip/route> print
Flags: D - dynamic; X - disabled, I - inactive, A - active; C - connect, S - static, r - ri
p, b - bgp, o - ospf, d - dhcp, v - vpn
Columns: DST-ADDRESS, GATEWAY, Distance
    DST-ADDRESS    GATEWAY D
DAC 10.1.1.0/24    ether1  0
DAC 172.16.1.0/30  ether2  0
DAC 192.168.1.0/24 bridge1 0
```

To fix this we need to add a route that tells the router what is the next device in the network to reach the destination.  In our example next hop is Router2, so we need to add a route with the gateway that points to the Router's 2 connected address. This type of route is known as a static route : 

```
[admin@MikroTik] > /ip route add dst-address=192.168.2.0/24 gateway=172.16.1.2
[admin@MikroTik] > /ip/route> print
Flags: D - dynamic; X - disabled, I - inactive, A - active; C - connect, S - static, r - ri
p, b - bgp, o - ospf, d - dhcp, v - vpn
Columns: DST-ADDRESS, GATEWAY,       Distance
        DST-ADDRESS    GATEWAY       D
    DAC 10.1.1.0/24    ether1        0
    DAC 172.16.1.0/30  ether2        0
    DAC 192.168.1.0/24 bridge1       0
0   AS  192.168.2.0/24 172.16.1.2
```

At this point packet from LAN1 will be successfully forwarded to LAN2, but we are not over yet. Router2 does not know how to reach LAN1, so any packet from LAN2 will be dropped on Router2. 

If we look again at the network diagram, we can clearly see that Router2 has only one point of exit. It is safe to assume that all other unknown networks should be reached over the link to Router1. The easiest way to do this is by adding a default route : To add a default route set destination 0.0.0.0/0 or leave it blank: 

```
/ip route add gateway=172.16.1.1
```

As we have seen from the example setup, there are different groups of routes, based on their origin and properties.
