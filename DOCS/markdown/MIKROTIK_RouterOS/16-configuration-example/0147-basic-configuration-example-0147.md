## Basic Configuration Example 

Basic Layer2 EVPN Vxlan configuration: 

1023 

```
/interface bridge
add name=bridge1 vlan-filtering=yes pvid=40
/interface bridge port
add bridge=bridge1 interface=sfp-sfpplus3 pvid=40
```

```
/ip address
```

```
add address=203.0.113.1 interface=lo
```
