## Inter-VLAN routing 

Many MikroTik's devices come with a built-in switch chip that can be used to greatly improve overall throughput when configured properly. Devices with a switch chip can be used as a router and a switch at the same time, this gives you the possibility to use a single device instead of multiple devices for your network. 

**==> picture [504 x 159] intentionally omitted <==**

For this type of setup to work, you must switch all required ports together 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether3 hw=yes
```
