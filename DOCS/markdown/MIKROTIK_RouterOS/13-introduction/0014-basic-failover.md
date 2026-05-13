## Basic failover 

First things first, since we have a local address space we need to masquerade LAN traffic on both uplinks: 

```
/ip/firewall/nat
add chain=srcnat action=masquerade out-interface=ether1
add chain=srcnat action=masquerade out-interface=ether2
```

Next we want to pick two hosts on the internet and make them reachable each on its own uplink. Generally you would pick hosts that are always supposed to be reachable, accepts ICMP, in this example we will use google DNS servers (8.8.8.8 and 8.8.4.4). 

```
/ip/route/
add dst-address=8.8.8.8 scope=10 gateway=10.111.0.1
add dst-address=8.8.4.4 scope=10 gateway=10.112.0.1
```

And add default routes recursively resolved over both hosts with ISP1 being the primary one (by having smaller distance): 

758 

```
/ip/route/
```

```
add distance=1 gateway=8.8.8.8 target-scope=11 check-gateway=ping
add distance=2 gateway=8.8.4.4 target-scope=11 check-gateway=ping
```
