## Dynamic Vrf-Lite route leaking 

With large enough setups static route leaking is not sufficient. Let's consider we have the same setup as in static route leaking example plus ipv6 addresses, just for demonstration. 

```
/ip address
add address=10.11.0.1/24 interface=sfp-sfpplus1
add address=10.12.0.1/24 interface=sfp-sfpplus2
```

```
# add VRF configuration
/ip vrf
add name=vrfTest1 interface=sfp-sfpplus1 place-before 0
add name=vrfTest2 interface=sfp-sfpplus2 place-before 0
```
