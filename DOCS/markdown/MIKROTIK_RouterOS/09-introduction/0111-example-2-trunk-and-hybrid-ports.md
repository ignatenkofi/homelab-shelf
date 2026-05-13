## Example 2 (Trunk and Hybrid Ports) 

554 

**==> picture [504 x 322] intentionally omitted <==**

Switch together the required ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```

Specify the VLAN ID that the switch must set on untagged (VLAN0) traffic for each access port: 

```
/interface ethernet switch ingress-vlan-translation
add ports=ether6 customer-vid=0 new-customer-vid=200
add ports=ether7 customer-vid=0 new-customer-vid=300
add ports=ether8 customer-vid=0 new-customer-vid=400
```

By specifying ports as tagged-ports, the switch will always send out packets as tagged packets with the corresponding VLAN ID. Add appropriate entries according to the diagram above: 

```
/interface ethernet switch egress-vlan-tag
add tagged-ports=ether2,ether7,ether8 vlan-id=200
add tagged-ports=ether2,ether6,ether8 vlan-id=300
add tagged-ports=ether2,ether6,ether7 vlan-id=400
```

Add entries to the VLAN table to specify VLAN memberships for each port and each VLAN ID: 

555 

```
/interface ethernet switch vlan
```

```
add ports=ether2,ether6,ether7,ether8 vlan-id=200 learn=yes
add ports=ether2,ether6,ether7,ether8 vlan-id=300 learn=yes
add ports=ether2,ether6,ether7,ether8 vlan-id=400 learn=yes
```

After a valid VLAN configuration has been set up, you can enable unknown/invalid VLAN filtering: 

```
/interface ethernet switch
```

```
set drop-if-invalid-or-src-port-not-member-of-vlan-on-ports=ether2,ether6,ether7,ether8
```
