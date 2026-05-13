## Example 1 (Trunk and Access ports) 

**==> picture [504 x 322] intentionally omitted <==**

Switch together the required ports: 

553 

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

**==> picture [13 x 13] intentionally omitted <==**

When an entry is created under `/interface ethernet switch ingress-vlan-translation` , then the switch chip will add a VLAN tag on ingress frames on the specified port. To remove the VLAN tag on the same port for egress frames, an `/interface ethernet switch egress-vlan-tag` entry should be created for the same VLAN ID where only tagged ports are specified. If a specific VLAN is forwarded only between access ports, the `/interface ethernet switch egress-vlan-tag` entry should still be created without any tagged ports. Another option is to create extra entries under `/interface ethernet switch egress-vlan-translation` menu to set untagged (VLAN0) traffic. 

You must also specify which VLANs should be sent out to the trunk port with a VLAN tag. Use the tagged-ports property to set up a trunk port: 

```
/interface ethernet switch egress-vlan-tag
add tagged-ports=ether2 vlan-id=200
add tagged-ports=ether2 vlan-id=300
add tagged-ports=ether2 vlan-id=400
```

Add entries to the VLAN table to specify VLAN memberships for each port and each VLAN ID: 

```
/interface ethernet switch vlan
add ports=ether2,ether6 vlan-id=200
add ports=ether2,ether7 vlan-id=300
add ports=ether2,ether8 vlan-id=400
```

After a valid VLAN configuration has been set up, you can enable unknown/invalid VLAN filtering: 

```
/interface ethernet switch
```

```
set drop-if-invalid-or-src-port-not-member-of-vlan-on-ports=ether2,ether6,ether7,ether8
```

**==> picture [13 x 13] intentionally omitted <==**

It is possible to use the built-in switch chip and the CPU at the same time to create a Switch-Router setup, where a device acts as a switch and as a router simultaneously. You can find a configuration example in the CRS-Router guide.
