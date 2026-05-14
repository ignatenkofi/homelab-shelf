## Private VLAN 

In some scenarios, you might need to forward all traffic to an uplink port while all other ports are isolated from each other. This kind of setup is called Privat e VLAN configuration, the Switch will forward all Ethernet frames directly to the uplink port allowing the Router to filter unwanted packets and limit access between devices that are behind switch ports. 

**==> picture [504 x 236] intentionally omitted <==**

To configure switch port isolation, you need to switch all required ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
add interface=sfp1 bridge=bridge1 hw=yes
add interface=ether1 bridge=bridge1 hw=yes
add interface=ether2 bridge=bridge1 hw=yes
add interface=ether3 bridge=bridge1 hw=yes
```

**==> picture [13 x 13] intentionally omitted <==**

By default, the bridge interface is configured with `protocol-mode` set to `rstp` . For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features. 

Override the egress port for each switch port that needs to be isolated (excluding the uplink port): 

```
/interface ethernet switch port-isolation
set ether1 forwarding-override=sfp1
set ether2 forwarding-override=sfp1
set ether3 forwarding-override=sfp1
```

**==> picture [13 x 13] intentionally omitted <==**

It is possible to set multiple uplink ports for a single switch chip, this can be done by specifying multiple interfaces and separating them with a comma. 

Isolated switch groups 

489 

In some scenarios you might need to isolate a group of devices from other groups, this can be done using the switch port isolation feature. This is useful when you have multiple networks but you want to use a single switch, with port isolation you can allow certain switch ports to be able to communicate through only a set of switch ports. In this example, devices on ether1-3 will only be able to communicate with devices that are on ether1-3 , while devices on ether4-5 will only be able to communicate with devices on ether4-5 ( ether1-3 is not able to communicate with ether4-5 ) 

**==> picture [13 x 13] intentionally omitted <==**

Port isolation is only available between ports that are members of the same switch. 

**==> picture [504 x 357] intentionally omitted <==**

To configure isolated switch groups you must first switch all ports: 

```
/interface bridge
add name=bridge
/interface bridge port
add bridge=bridge1 interface=ether1 hw=yes
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether3 hw=yes
add bridge=bridge1 interface=ether4 hw=yes
add bridge=bridge1 interface=ether5 hw=yes
```

**==> picture [13 x 13] intentionally omitted <==**

By default, the bridge interface is configured with `protocol-mode` set to `rstp` . For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features. 

Then specify in the `forwarding-override` property all ports that you want to be in the same isolated switch group (except the port on which you are applying the property), for example, to create an isolated switch group for A devices: 

490 

```
/interface ethernet switch port-isolation
set ether1 forwarding-override=ether2,ether3
set ether2 forwarding-override=ether1,ether3
set ether3 forwarding-override=ether1,ether2
```

To create an isolated switch group for B devices: 

```
/interface ethernet switch port-isolation
set ether4 forwarding-override=ether5
set ether5 forwarding-override=ether4
```
