## MAC Based Mirroring 

This example will mirror incoming traffic with 64:D1:54:D9:27:E6 MAC destination or source address from the ether1 interface, and send copies to the ether3 interface. 

```
/interface ethernet switch
set switch1 mirror-target=ether3
/interface ethernet switch rule
```

```
add mirror=yes ports=ether1 switch=switch1 dst-mac-address=64:D1:54:D9:27:E6/FF:FF:FF:FF:FF:FF
add mirror=yes ports=ether1 switch=switch1 src-mac-address=64:D1:54:D9:27:E6/FF:FF:FF:FF:FF:FF
```

402
