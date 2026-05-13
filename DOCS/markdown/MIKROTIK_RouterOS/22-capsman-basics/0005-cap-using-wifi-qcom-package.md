## CAP using "wifi-qcom" package: 

```
/interface bridge
add name=bridgeLocal
/interface wifi datapath
add bridge=bridgeLocal comment=defconf disabled=no name=capdp
/interface wifi
set [ find default-name=wifi1 ] configuration.manager=capsman datapath=capdp disabled=no
set [ find default-name=wifi2 ] configuration.manager=capsman datapath=capdp disabled=no
/interface bridge port
add bridge=bridgeLocal comment=defconf interface=ether1
add bridge=bridgeLocal comment=defconf interface=ether2
add bridge=bridgeLocal comment=defconf interface=ether3
add bridge=bridgeLocal comment=defconf interface=ether4
add bridge=bridgeLocal comment=defconf interface=ether5
/interface wifi cap
set discovery-interfaces=bridgeLocal enabled=yes slaves-datapath=capdp
/ip dhcp-client
add interface=bridgeLocal disabled=no
```

1346
