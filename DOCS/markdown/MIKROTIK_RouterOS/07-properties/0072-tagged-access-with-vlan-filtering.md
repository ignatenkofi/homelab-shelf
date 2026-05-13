## Tagged access with VLAN filtering 

In case VLAN filtering is used and access with tagged traffic is desired, additional steps are required. In this example, VLAN 99 will be used to access the device. A VLAN interface on the bridge must be created and an IP address must be assigned to it. 

```
/interface vlan
add interface=bridge1 name=MGMT vlan-id=99
/ip address
add address=192.168.99.1/24 interface=MGMT
```

378 

For example, if you want to allow access to the device from ports ether3 , ether4, sfp-sfpplus1 using tagged VLAN 99 traffic, then you must add this entry to the VLAN table. Note that the bridge1 interface is also included in the tagged port list: 

```
/interface bridge vlan
```

```
add bridge=bridge1 tagged=bridge1,ether3,ether4,sfp-sfpplus1 vlan-ids=99
```

After that you can enable VLAN filtering: 

```
/interface bridge set bridge1 vlan-filtering=yes
```
