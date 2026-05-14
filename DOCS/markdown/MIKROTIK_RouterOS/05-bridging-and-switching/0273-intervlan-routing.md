## InterVLAN Routing 

558 

**==> picture [504 x 323] intentionally omitted <==**

InterVLAN routing configuration consists of two main parts – VLAN tagging in switch-chip and routing in RouterOS. This configuration can be used in many applications by combining it with a DHCP server, Hotspot, PPP, and other features for each VLAN. 

Switch together the required ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```

Set VLAN tagging on the CPU port for all VLANs to make packets tagged before they are routed: 

```
/interface ethernet switch egress-vlan-tag
add tagged-ports=switch1-cpu vlan-id=200
add tagged-ports=switch1-cpu vlan-id=300
add tagged-ports=switch1-cpu vlan-id=400
```

add ingress VLAN translation rules to ensure that the correct VLAN ID assignment is done on access ports: 

```
/interface ethernet switch ingress-vlan-translation
add ports=ether6 customer-vid=0 new-customer-vid=200
add ports=ether7 customer-vid=0 new-customer-vid=300
add ports=ether8 customer-vid=0 new-customer-vid=400
```

Create the VLAN interfaces on top of the bridge interface: 

559 

```
/interface vlan
```

```
add name=VLAN200 interface=bridge1 vlan-id=200
add name=VLAN300 interface=bridge1 vlan-id=300
add name=VLAN400 interface=bridge1 vlan-id=400
```

**==> picture [13 x 13] intentionally omitted <==**

Make sure the VLAN interfaces are created on top of the bridge interface instead of any of the physical interfaces. If the VLAN interfaces are created on a slave interface, then the packet might not be received correctly, and therefore routing might fail. More detailed information can be found in the VLAN interface on a slave interface manual page. 

Add IP addresses on created VLAN interfaces. In this example, three 192.168.x.1 addresses are added to VLAN200, VLAN300, and VLAN400 interfaces: 

```
/ip address
add address=192.168.20.1/24 interface=VLAN200
add address=192.168.30.1/24 interface=VLAN300
add address=192.168.40.1/24 interface=VLAN400
```
