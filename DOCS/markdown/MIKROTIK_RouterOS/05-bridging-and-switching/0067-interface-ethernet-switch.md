## `/interface ethernet switch` 

```
set switch1 mirror-target=ether3 mirror-source=none
/interface ethernet switch rule
```

```
add mirror=yes ports=ether1 switch=switch1 src-address=192.168.88.0/24
add mirror=yes ports=ether1 switch=switch1 dst-address=192.168.88.0/24
```

There are other options as well, check the ACL section to find out all possible parameters that can be used to match packets.
