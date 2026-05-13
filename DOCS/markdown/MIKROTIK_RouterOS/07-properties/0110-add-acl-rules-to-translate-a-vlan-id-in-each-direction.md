## Add ACL rules to translate a VLAN ID in each direction: 

```
/interface ethernet switch rule
```

```
add new-dst-ports=ether2 new-vlan-id=20 ports=ether1 switch=switch1 vlan-id=10
add new-dst-ports=ether1 new-vlan-id=10 ports=ether2 switch=switch1 vlan-id=20
```
