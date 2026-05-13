## Configuration 

597 

The following configuration is relevant to R1 and R2 : 

```
/interface bonding
```

```
add mode=802.3ad name=bond1 slaves=ether1,ether2 transmit-hash-policy=layer-2-and-3
/ip address
add address=192.168.1.X/24 interface=bond1
```

While the following configuration is relevant to AP1 , AP2 , ST1, and ST2 , where X corresponds to an IP address for each device. 

```
/interface bridge
add name=bridge1 protocol-mode=none
/interface bridge port
add interface=ether1 bridge=bridge1
add interface=wlan1 bridge=bridge1
/ip address
add address=192.168.1.X/24 interface=bridge1
```
