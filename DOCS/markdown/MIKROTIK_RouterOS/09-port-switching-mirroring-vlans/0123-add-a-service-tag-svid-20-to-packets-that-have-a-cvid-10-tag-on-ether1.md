## Add a service tag SVID 20 to packets that have a CVID 10 tag on ether1 : 

```
/interface ethernet switch ingress-vlan-translation
add customer-vid=10 new-service-vid=20 ports=ether1
```
