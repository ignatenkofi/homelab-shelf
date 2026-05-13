## Interface Lists 

Two interface lists will be used WAN and LAN for easier future management purposes. Interfaces connected to the global internet should be added to the WAN list, in this case, it is ether1! 

```
/interface list
  add comment=defconf name=WAN
  add comment=defconf name=LAN
/interface list member
  add comment=defconf interface=bridge list=LAN
  add comment=defconf interface=ether1 list=WAN
```
