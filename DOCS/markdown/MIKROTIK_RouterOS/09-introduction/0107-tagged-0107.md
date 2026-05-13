## Tagged 

Allowing only tagged traffic to have management access to the device through a specific port is a much better practice. For example, to allow only VLAN99 to access the device through ether2 you should first add an entry to the VLAN table, which will allow the selected port and the CPU port ( switch1-cpu ) to forward the selected VLAN ID, therefore allowing management access: 

```
/interface ethernet switch vlan
```

```
add ports=ether2,switch1-cpu vlan-id=99
```

Packets that will be sent out from the CPU, for example, ping replies will not have a VLAN tag, to solve this you need to specify which ports should always send out packets with a VLAN tag for a specific VLAN ID: 

```
/interface ethernet switch egress-vlan-tag
add tagged-ports=ether2,switch1-cpu vlan-id=99
```

After a valid VLAN99 configuration has been set up, you can enable unknown/invalid VLAN filtering, which will not allow the management access through different ports than specified in the VLAN table: 

```
/interface ethernet switch
```

```
set drop-if-invalid-or-src-port-not-member-of-vlan-on-ports=ether2,ether3,ether4,ether5
```

In this example VLAN99 will be used to access the device, a VLAN interface on the bridge must be created and an IP address must be assigned to it. 

```
/interface vlan
add interface=bridge1 name=MGMT vlan-id=99
/ip address
add address=192.168.99.1/24 interface=MGMT
```

552
