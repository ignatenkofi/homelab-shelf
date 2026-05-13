## Ingress VLAN translation 

It is possible to translate a certain VLAN ID to a different VLAN ID using ACL rules on an ingress port. In this example we create two ACL rules, allowing bidirectional communication. This can be done by doing the following. 

Create a new bridge and add ports to it with hardware offloading: 

399 

```
/interface bridge
```

```
add name=bridge1 vlan-filtering=no
/interface bridge port
add interface=ether1 bridge=bridge1 hw=yes
add interface=ether2 bridge=bridge1 hw=yes
```
