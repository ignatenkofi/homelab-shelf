## DHCP Server Setup 

To setup 2 DHCP Servers on the DHCP-Server router add 2 pools. For networks 192.168.1.0/24 and 192.168.2.0: 

```
/ip pool add name=Local1-Pool ranges=192.168.1.11-192.168.1.100
/ip pool add name=Local2-Pool ranges=192.168.2.11-192.168.2.100
[admin@DHCP-Server] ip pool> print
 # NAME                                         RANGES
 0 Local1-Pool                                  192.168.1.11-192.168.1.100
 1 Local2-Pool                                  192.168.2.11-192.168.2.100
[admin@DHCP-Server] ip pool>
```
