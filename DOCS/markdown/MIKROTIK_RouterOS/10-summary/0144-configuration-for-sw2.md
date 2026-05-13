## Configuration for SW2: 

```
/interface bridge
add name=bridge priority=0x2000
/interface bridge port
add bridge=bridge interface=ether1
add bridge=bridge interface=ether2
add bridge=bridge interface=ether3
```
