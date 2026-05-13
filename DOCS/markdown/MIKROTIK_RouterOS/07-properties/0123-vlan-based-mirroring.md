## VLAN Based Mirroring 

Using ACL rules, it is possible to mirror packets from multiple interfaces using the `ports` setting. Additionally, you can specify more detailed criteria such as VLAN ID, MAC/IP address or TCP/UDP port. Only ingress packets are mirrored to `mirror-target` interface. This example will mirror incoming VLAN 11 traffic from the ether2 interface, and send copies to the ether3 interface. To use an ACL rule with a `vlan-id` matcher, you need to have bridge vlanfiltering enabled. 

```
/interface bridge
set bridge1 vlan-filtering=yes
/interface ethernet switch
set switch1 mirror-target=ether3
/interface ethernet switch rule
add mirror=yes ports=ether1 switch=switch1 vlan-id=11
```
