## A router on site 2: 

```
/ip address add address=172.16.1.2/30 interface=myGre
/ip route add dst-address=10.1.101.0/24 gateway=172.16.1.1
```

At this point, both sites have Layer 3 connectivity over the GRE tunnel. 

1185
