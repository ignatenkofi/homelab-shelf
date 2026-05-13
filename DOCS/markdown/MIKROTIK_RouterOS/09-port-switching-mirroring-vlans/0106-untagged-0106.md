## Untagged 

If invalid VLAN filtering is not enabled, management access to the device using tagged or untagged ( VLAN 0 ) traffic is already allowed from any port, though this is not a good practice, this can cause security issues and can cause the device's CPU to be overloaded in certain situations (most commonly with a broadcast type of traffic). 

If you intend to use invalid VLAN filtering (which you should), then ports, from which you are going to access the switch, must be added to the VLAN table for untagged ( VLAN 0 ) traffic, for example, in case you want to access the switch from ether2 : 

```
/interface ethernet switch vlan
add vlan-id=0 ports=ether2,switch1-cpu
```
