## Basic IGMP snooping configuration 

The first example consists only of a single IGMP snooping bridge, a single multicast source device, and a couple of multicast client devices. See a network scheme below. 

520 

**==> picture [504 x 361] intentionally omitted <==**

First, create a bridge interface with enabled IGMP snooping. In this example, there is no active IGMP querier (no multicast router or proxy), so a local IGMP querier must be enabled on the same bridge. This can be done with a `multicast-querier` setting. If there is no active IGMP querier in the LAN, the unregistered IP multicast will be flooded and multicast entries will always timeout from the multicast database. 

```
/interface bridge
```

```
add igmp-snooping=yes multicast-querier=yes name=bridge1
```

Then add the necessary interfaces as bridge ports. 

```
/interface bridge port
add bridge=bridge1 interface=ether2
add bridge=bridge1 interface=ether3
add bridge=bridge1 interface=ether4
add bridge=bridge1 interface=ether5
```

The basic IGMP snooping configuration is finished. Use " `/interface bridge mdb print"` command to monitor the active multicast groups. If necessary, you can configure an IP address and DHCP server on the same bridge interface.
