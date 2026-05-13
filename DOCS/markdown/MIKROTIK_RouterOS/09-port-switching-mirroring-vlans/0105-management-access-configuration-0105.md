## Management access configuration 

In general, switches are only supposed to forward packets by using the built-in switch chip, but not allow access to the device itself for security reasons. It is possible to use the device's serial port for management access, but in most cases, such an access method is not desired and access using an IP address is more suitable. In such cases, you will need to configure management access. 

551 

In all types of management access it is assumed that ports must be switched together, use the following commands to switch together the required ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether3 hw=yes
add bridge=bridge1 interface=ether4 hw=yes
add bridge=bridge1 interface=ether5 hw=yes
```

You should also assign an IP address to the bridge interface so the device is reachable using an IP address (the device is also reachable using a MAC address): 

```
/ip address
add address=192.168.88.1/24 interface=bridge1
```
