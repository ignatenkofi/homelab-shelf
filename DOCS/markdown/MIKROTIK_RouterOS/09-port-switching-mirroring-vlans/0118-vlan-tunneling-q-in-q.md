## VLAN Tunneling (Q-in-Q) 

This example covers a typical VLAN tunneling use case where service provider devices add another VLAN tag for independent forwarding in the meantime allowing customers to use their own VLANs. 

**==> picture [13 x 12] intentionally omitted <==**

This example contains only the Service VLAN tagging part. It is recommended to additionally set Unknown/Invalid VLAN filtering configuration on ports. 

560 

**==> picture [504 x 221] intentionally omitted <==**

CRS-1 : The first switch on the edge of the service provider network has to properly identify traffic from the customer VLAN ID on port and assign a new service VLAN ID with ingress VLAN translation rules. VLAN trunk port configuration for service provider VLAN tags is in the same `egress-vlan-tag` tabl e. The main difference from basic Port-Based VLAN configuration is that the CRS switch-chip has to be set to do forwarding according to service (outer) VLAN ID instead of customer (inner) VLAN ID. 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether1 hw=yes
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether9 hw=yes
```

```
/interface ethernet switch ingress-vlan-translation
add customer-vid=200 new-service-vid=400 ports=ether1
add customer-vid=300 new-service-vid=500 ports=ether2
```

```
/interface ethernet switch egress-vlan-tag
add tagged-ports=ether9 vlan-id=400
add tagged-ports=ether9 vlan-id=500
```

```
/interface ethernet switch
```

```
set bridge-type=service-vid-used-as-lookup-vid
```

CRS-2 : The second switch in the service provider network requires only switched ports to do forwarding according to service (outer) VLAN ID instead of customer (inner) VLAN ID. 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether9 hw=yes
add bridge=bridge1 interface=ether10 hw=yes
```

```
/interface ethernet switch
```

```
set bridge-type=service-vid-used-as-lookup-vid
```
