## We can say that connected network is reachable on specific vrf by setting gateway "interface@vrf" 

```
# add vrf routes
/ip route
add dst-address=10.11.0.0/24 gateway="sfp-sfpplus1@vrfTest1" routing-table=vrfTest2
add dst-address=10.12.0.0/24 gateway="sfp-sfpplus2@vrfTest2" routing-table=vrfTest1
```
