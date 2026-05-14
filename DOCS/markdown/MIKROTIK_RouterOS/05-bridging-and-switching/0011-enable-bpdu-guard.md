## Enable BPDU guard 

In this example, if ether1 receives a BPDU, it will block the port and will require you to manually re-enable it. 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether1 bpdu-guard=yes
add bridge=bridge1 interface=ether2
```
