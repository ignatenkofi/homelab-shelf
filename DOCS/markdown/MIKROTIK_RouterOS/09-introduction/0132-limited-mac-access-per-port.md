## Limited MAC Access per Port 

Disabling MAC learning and configuring static MAC addresses gives the ability to control what exact devices can communicate to CRS1xx/2xx switches and through them. 

Configuration requires a group of switched ports, disabled MAC learning on those ports, and static UFDB entries: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether6 hw=yes learn=no unknown-unicast-flood=no
add bridge=bridge1 interface=ether7 hw=yes learn=no unknown-unicast-flood=no
```

```
/interface ethernet switch unicast-fdb
```

```
add mac-address=4C:5E:0C:00:00:01 port=ether6 svl=yes
add mac-address=D4:CA:6D:00:00:02 port=ether7 svl=yes
```
