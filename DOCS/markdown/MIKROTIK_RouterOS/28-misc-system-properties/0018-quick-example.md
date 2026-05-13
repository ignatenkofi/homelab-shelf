## Quick Example 

Here we will use a simple ICMP check to host with IP 8.8.8.8: 

```
[admin@MikroTik] > /tool/netwatch add host=8.8.8.8 interval=30s up-script=":log info \"Ping to 8.8.8.8
successful\""
```

Afterward, in the logging section we can see Netwatch executed script: 

```
[admin@MikroTik] > log print where message~"8.8.8.8"
08:03:26 script,info Ping to 8.8.8.8 successful
```

1794
