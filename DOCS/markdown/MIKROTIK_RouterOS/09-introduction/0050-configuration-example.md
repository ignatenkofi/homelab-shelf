## Configuration example 

This configuration example creates a single VXLAN tunnel between two statically configured VTEP endpoints. 

First, create VXLAN interfaces on both routers. 

```
/interface vxlan
add name=vxlan1 port=4789 vni=10
```

Then configure VTEPs on both routers with respective IPv4 destination addresses. Both devices should have an active route toward the destination address. 

```
# Router1
/interface vxlan vteps
add interface=vxlan1 remote-ip=192.168.10.10
# Router2
/interface vxlan vteps
add interface=vxlan1 remote-ip=192.168.20.20
```

The configuration is complete. It is possible to include the VXLAN interface into a bridge with other Ethernet interfaces.
