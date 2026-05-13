## Configuration 

For both devices DeviceA and DeviceB there should be a very similar configuration. 

```
/interface bridge
add name=bridge1 protocol-mode=rstp
/interface bridge port
add interface=ether1 bridge=bridge1
add interface=eoip1 bridge=bridge1
```

596
