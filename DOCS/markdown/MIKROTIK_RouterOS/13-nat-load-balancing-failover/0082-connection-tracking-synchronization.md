## Connection tracking synchronization 

Similar to different High availability features, RouterOS v7 supports VRRP connection tracking synchronization. 

The VRRP connection tracking synchronization requires that RouterOS connection tracking is running. By default, connection tracking is working in `auto` mode. If VRRP devices do not contain any firewall rules, you need to manually enable connection tracking: 

```
/ip/firewall/connection/tracking/set enabled=yes
```

To sync connection tracking entries configure the device as follows: 

```
/interface/vrrp/set vrrp1 sync-connection-tracking=yes
```

Verify configuration in the logging section: 

```
16:14:06 vrrp,info vrrp1 now MASTER, master down timer
16:14:06 vrrp,info vrrp1 stop CONNTRACK
16:14:06 vrrp,info vrrp1 starting CONNTRACK MASTER
```

Connection tracking entries are synchronized only from the Master to the Backup device. 

When both **`sync-connection-tracking`** and **`preemption-mode`** are enabled, and a router with higher VRRP priority becomes online, the connections get synchronized first, and only then the router with higher priority becomes the VRRP master. 

**==> picture [13 x 13] intentionally omitted <==**

If multiple VRRP interfaces are configured between two units and `sync-connection-tracking=yes` is required, it must be enabled only on one of the VRRP interfaces, preferably the one designated as the `group-authority` .
