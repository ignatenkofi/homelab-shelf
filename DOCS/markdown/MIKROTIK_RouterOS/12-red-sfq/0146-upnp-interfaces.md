## UPnP Interfaces 

```
/ip upnp interfaces
```

Property Description 

750 

interface (string; Default: ) Interface name on which uPnP will be running type (external | internal; Default: no ) UPnP interface type: `external` - the interface a global IP address is assigned to `internal` - router's local interface the clients are connected to forced-external-ip (Ip; Default: ) Allow specifying what public IP to use if the external interface has more than one IP available. 

**==> picture [13 x 13] intentionally omitted <==**

In more complex setups with VLANs, where the VLAN interface is considered as the LAN interface, the VLAN interface itself should be specified as the internal interface for UPnP to work properly.
