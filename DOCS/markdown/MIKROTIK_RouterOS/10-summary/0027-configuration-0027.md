## Configuration 

The following configuration is relevant to SW1 and SW2 : 

```
/interface bonding
add mode=802.3ad name=bond1 slaves=ether1,ether2
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=bond1
add bridge=bridge1 interface=sfp-sfpplus1
```
