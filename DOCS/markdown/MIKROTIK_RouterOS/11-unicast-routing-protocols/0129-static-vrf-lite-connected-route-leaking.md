## Static VRF-Lite Connected route leaking 

Sometimes it is necessary to access directly connected resources from another vrf. In our example setup we have two connected networks each in its own VRF. And we want to allow client1 to be able to access client2. 

```
                   +-----------------+
                   |+-vrf1-+ +-vrf2-+|
client1(*.2)-------||ip *.1| |ip *.1||-------client2(*.2)
   (10.11.0.0/24)  |+------+ +------+|   (10.12.0.0/24)
```

```
                   +-----------------+
```

1040 

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
