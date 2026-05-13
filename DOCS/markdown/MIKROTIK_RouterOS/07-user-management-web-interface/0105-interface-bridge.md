## `/interface bridge` 

```
add name=bridge1 vlan-filtering=yes
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```

Add VLANs in the Bridge VLAN table and specify ports:
