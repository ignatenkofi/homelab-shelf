## Untagged access without VLAN filtering 

In case VLAN filtering will not be used and access with untagged traffic is desired, the only requirement is to create an IP address on the bridge interface. 

```
/ip address
add address=192.168.99.1/24 interface=bridge1
```
