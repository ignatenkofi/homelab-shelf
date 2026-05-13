## Create edge ports 

Setting a bridge port as an edge port will restrict it from sending BPDUs and will ignore any received BPDUs: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether1 edge=yes
add bridge=bridge1 interface=ether2
```
