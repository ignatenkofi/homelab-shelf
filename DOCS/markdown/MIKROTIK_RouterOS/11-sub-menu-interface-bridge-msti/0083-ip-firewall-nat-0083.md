## `/ip firewall nat` 

```
add action=endpoint-independent-nat chain=srcnat out-interface=WAN protocol=udp
```

This mapping allows running source-independent filtering, which allows forwarding packets from any source from WAN to mapped internal IP and port. The following rule enables filtering:
