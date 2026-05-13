## Ros_Leaf_3 

```
/ip address
add address=203.0.255.133 interface=lo
add address=172.16.3.2/30 interface=ether10
```

```
/routing ospf instance
add name=evpn_underlay
/routing ospf area
add disabled=no instance=evpn_underlay name=evpn-underlay-bb
/routing ospf interface-template
add area=evpn-underlay-bb disabled=no networks=172.16.0.0/16
add area=evpn-underlay-bb disabled=no interfaces=lo passive
```
