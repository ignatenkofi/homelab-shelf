## Configuration for SW1: 

```
/interface bridge
add name=bridge priority=0x1000
/interface bridge port
add bridge=bridge interface=ether1 priority=0x60
add bridge=bridge interface=ether2 priority=0x50
add bridge=bridge interface=ether3 priority=0x40
add bridge=bridge interface=ether4 priority=0x30
add bridge=bridge interface=ether5
```
