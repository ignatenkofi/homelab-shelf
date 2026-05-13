## Bridging and listing 

Bridge all ports: 

```
/interface bridge
add auto-mac=no comment=defconf name=bridge
/interface bridge port
add interface=all bridge=bridge
```

And, ensure, that the bridge is listed as "LAN" interface, so that the firewall rules do not block access to the AP's management: 

```
/interface list member
add comment=defconf interface=bridge list=LAN
```

That is, of course, if you have proper firewall and access restrictions added on the main router. Otherwise, restrict it.
