## Using bridge on Linux 

If Linux bridge supports IGMP snooping, and there are problems with IPv6 traffic it is required to disable that feature as it interacts with MLD packets (multicast) and is not passing them through. 

```
echo -n 0 > /sys/class/net/vmbr0/bridge/multicast_snooping
```
