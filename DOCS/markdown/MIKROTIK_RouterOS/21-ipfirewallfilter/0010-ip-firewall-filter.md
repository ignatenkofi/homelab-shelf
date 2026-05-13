## `/ip firewall filter` 

```
add action=accept chain=input comment="allow WireGuard" dst-port=13231 protocol=udp place-before=1
```

To allow remote devices to connect to the RouterOS services (e.g. request DNS), allow the WireGuard subnet in input chain.
