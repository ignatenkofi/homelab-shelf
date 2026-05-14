## Configuration lines 

**==> picture [13 x 13] intentionally omitted <==**

These rules are only an improvement for firewall, do not forget to properly secure your device. 

```
/ip firewall address-list
add list=ddos-attackers
add list=ddos-targets
/ip firewall filter
add action=return chain=detect-ddos dst-limit=32,32,src-and-dst-addresses/10s
add action=add-dst-to-address-list address-list=ddos-targets address-list-timeout=10m chain=detect-ddos
add action=add-src-to-address-list address-list=ddos-attackers address-list-timeout=10m chain=detect-ddos
/ip firewall raw
```

```
add action=drop chain=prerouting dst-address-list=ddos-targets src-address-list=ddos-attackers
```
