## Other clients services 

RouterOS might have other services enabled (they are disabled by default RouterOS configuration). MikroTik caching proxy, socks, UPnP, and cloud services: 

```
/ip proxy set enabled=no
/ip socks set enabled=no
/ip upnp set enabled=no
/ip cloud set ddns-enabled=no update-time=no
```
