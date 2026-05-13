## Adding IP Address 

Consider a setup where two routers are directly connected with the cable and we do not want to waste address space: 

R1 configuration: 

```
/ip address
```

```
add address=10.1.1.1/32 interface=ether1 network=172.16.1.1
```
