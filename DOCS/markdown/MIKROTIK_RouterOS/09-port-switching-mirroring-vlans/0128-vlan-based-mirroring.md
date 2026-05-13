## VLAN Based Mirroring 

The second example requires ports to be switched in a group. Mirroring configuration sets the ether5 port as a mirror0 analyzer port and sets the mirror0 port to be used when mirroring from VLAN occurs. VLAN table entry enables mirroring only for VLAN 300 traffic between ether2 and ether7 ports. 

563 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
```

```
/interface ethernet switch
set ingress-mirror0=ether5 vlan-uses=mirror0
```

```
/interface ethernet switch vlan
add ports=ether2,ether7 vlan-id=300 learn=yes ingress-mirror=yes
```
