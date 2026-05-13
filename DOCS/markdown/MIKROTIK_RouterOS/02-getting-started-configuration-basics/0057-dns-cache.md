## DNS cache 

A router might have DNS cache enabled, which decreases the resolving time for DNS requests from clients to remote servers. In case DNS cache is not required on your router or another router is used for such purposes, disable it: 

```
/ip dns set allow-remote-requests=no
```
