## Configuration 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 hw=yes interface=ether1 learn=yes
add bridge=bridge1 hw=yes interface=ether2 learn=yes
```
