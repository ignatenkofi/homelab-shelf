## Block access to specific websites 

This script is useful if you want to block certain websites but you don't want to use a web proxy. 

This example looks at entries "Rapidshare" and "youtube" in the DNS cache and adds IPs to the address list named "restricted". Before you begin, you must set up a router to catch all DNS requests: 

```
/ip firewall nat
```

```
add action=redirect chain=dstnat comment=DNS dst-port=53 protocol=tcp to-ports=53
add action=redirect chain=dstnat dst-port=53 protocol=udp to-ports=53
```
