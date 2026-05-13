## Tagged access without VLAN filtering 

In case VLAN filtering will not be used and access with tagged traffic is desired, create a routable VLAN interface on the bridge and add an IP address on the VLAN interface. 

```
/interface vlan
add interface=bridge1 name=MGMT vlan-id=99
/ip address
add address=192.168.99.1/24 interface=MGMT
```
