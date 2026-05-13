## OVPN Server 

```
/interface ovpn-server
```

An interface is created for each tunnel established to the given server. There are two types of interfaces in the OVPN server's configuration 

Static interfaces are added administratively if there is a need to reference the particular interface name (in firewall rules or elsewhere) created for the particular user. 

Dynamic interfaces are added to this list automatically whenever a user is connected and its username does not match any existing static entry (or in case the entry is active already, as there can not be two separate tunnel interfaces referenced by the same name). 

Dynamic interfaces appear when a user connects and disappear once the user disconnects, so it is impossible to reference the tunnel created for that use in router configuration (for example, in the firewall), so if you need a persistent rule for that user, create a static entry for him/her. Otherwise, it is safe to use dynamic configuration. 

**==> picture [13 x 13] intentionally omitted <==**

After upgrade to 7.17 version ovpn server will receive its configuration, due to multiple server support. 

An disabled ovpn server with added mac will appear in configuration: 

/interface ovpn-server server add mac-address=99:99:99:99:99:99 name=ovpn-server1 

**==> picture [13 x 13] intentionally omitted <==**

In both cases PPP users must be configured properly - static entries do not replace PPP configuration.
