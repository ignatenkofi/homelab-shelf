## Other Services 

A bandwidth server is used to test throughput between two MikroTik routers. Disable it in the production environment. 

```
/tool bandwidth-server set enabled=no
```

A router might have DNS cache enabled, which decreases resolving time for DNS requests from clients to remote servers. In case DNS cache is not required on your router or another router is used for such purposes, disable it. 

```
/ip dns set allow-remote-requests=no
```

It is good practice to disable all unused interfaces on your router, in order to decrease unauthorized access to your router. 

```
/interface print
/interface set ether13 disabled=yes
```
