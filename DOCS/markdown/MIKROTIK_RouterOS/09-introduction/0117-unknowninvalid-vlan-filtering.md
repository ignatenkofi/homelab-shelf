## Unknown/Invalid VLAN filtering 

VLAN membership is defined in the VLAN table. Adding entries with VLAN ID and ports makes that VLAN traffic valid on those ports. After a valid VLAN configuration has been set up, unknown/invalid VLAN filtering can be enabled. This VLAN filtering configuration example applies to the InterVLAN Routing s etup. 

```
/interface ethernet switch vlan
add ports=switch1-cpu,ether6 vlan-id=200
add ports=switch1-cpu,ether7 vlan-id=300
add ports=switch1-cpu,ether8 vlan-id=400
```

Option 1: disable invalid VLAN forwarding on specific ports (more common): 

```
/interface ethernet switch
```

```
set drop-if-invalid-or-src-port-not-member-of-vlan-on-ports=ether2,ether6,ether7,ether8
```

Option 2: disable invalid VLAN forwarding on all ports: 

```
/interface ethernet switch
set forward-unknown-vlan=no
```

**==> picture [13 x 13] intentionally omitted <==**

Using multiple bridges on a single switch chip with enabled unknown/invalid VLAN filtering can cause unexpected behavior. You should always use a single bridge configuration whenever using VLAN filtering. If port isolation is required, then the port isolation feature should be used instead of using multiple bridges.
