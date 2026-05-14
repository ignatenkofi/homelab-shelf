## CRS-3 : The third switch has a similar configuration to CRS-1: 

Ports in a switch group using a bridge; 

Ingress VLAN translation rules to define new service VLAN assignments on ports; tagged-ports for service provider VLAN trunks; 

CRS switch-chip set to use service VLAN ID in switching lookup. 

561 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether3 hw=yes
add bridge=bridge1 interface=ether4 hw=yes
add bridge=bridge1 interface=ether10 hw=yes
```

```
/interface ethernet switch ingress-vlan-translation
add customer-vid=200 new-service-vid=400 ports=ether3
add customer-vid=300 new-service-vid=500 ports=ether4
```

```
/interface ethernet switch egress-vlan-tag
add tagged-ports=ether10 vlan-id=400
add tagged-ports=ether10 vlan-id=500
```

```
/interface ethernet switch
set bridge-type=service-vid-used-as-lookup-vid
```
