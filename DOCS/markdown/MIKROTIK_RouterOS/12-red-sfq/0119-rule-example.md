## Rule Example 

These rules will capture TCP/UDP traffic that was going through the router when the connection speed was below 100kbps: 

```
/ip firewall filter
```

```
add action=accept chain=forward connection-rate=0-100k protocol=tcp
add action=accept chain=forward connection-rate=0-100k protocol=udp
```
