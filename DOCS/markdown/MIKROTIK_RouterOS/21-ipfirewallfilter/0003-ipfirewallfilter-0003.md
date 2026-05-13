## `/ip/firewall/filter` 

```
add action=accept chain=input dst-port=13231 protocol=udp src-address=192.168.90.1
```

Additionally, it is possible that the "forward" chain restricts the communication between the subnets as well, so such traffic should be accepted before any drop rules as well.
