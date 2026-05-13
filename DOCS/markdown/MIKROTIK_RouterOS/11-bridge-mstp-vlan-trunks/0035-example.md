## Example 

For example, for SOHO routers with factory default configuration, you could FastTrack all LAN traffic with this one rule placed at the top of the Firewall Filter. The same configuration accept rule is required: 

631 

```
/ip firewall filter add chain=forward action=fasttrack-connection connection-state=established,related
/ip firewall filter add chain=forward action=accept connection-state=established,related
```

**==> picture [13 x 13] intentionally omitted <==**

Connection is FastTracked until the connection is closed, timed-out, or router is rebooted. Dummy rules will disappear only after FastTrack firewall rules will be deleted/disabled and the router rebooted. While FastPath and FastTrack both are enabled on the device only one can be active at a time. 

**==> picture [13 x 13] intentionally omitted <==**

Queues (except Queue Trees parented to interfaces), firewall filter, and mangle rules will not be applied for FastTracked traffic.
