## Ros_Leaf_3 

Just for demonstration purposes, on RouterOS leaf we will be sending vlan tagged traffic to the host. 

VXLAN learning should be disabled as we are using BGP EVPN for discovery. 

```
/interface bridge
add name=bridge1 pvid=10 vlan-filtering=yes
/interface vxlan
add bridge=bridge1 bridge-pvid=10 learning=no local-address=203.0.255.133 mac-address=C2:16:F6:B2:CC:D3
name=vxlan1 vni=1010
/interface bridge port
add bridge=bridge1 interface=ether11 pvid=10
/ip address
add address=192.168.10.133/24 interface=bridge1
/routing bgp evpn
```

```
add disabled=no export.route-targets=1010:1010 import.route-targets=1010:1010 instance=bgp-instance-1 name=bgp-
evpn-1 vni=1010
```
