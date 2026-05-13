## Bandwidth Limiting 

Both Ingress Port policer and Shaper provide bandwidth limiting features for CRS switches: 

Ingress Port Policer sets RX limit on port: 

```
/interface ethernet switch ingress-port-policer
add port=ether5 meter-unit=bit rate=10M
```

Shaper sets TX limit on port: 

```
/interface ethernet switch shaper
add port=ether5 meter-unit=bit rate=10M
```
