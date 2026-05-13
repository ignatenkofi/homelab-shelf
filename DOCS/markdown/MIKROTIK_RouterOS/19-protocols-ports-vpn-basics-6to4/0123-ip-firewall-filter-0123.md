## `/ip firewall filter` 

```
add action=drop chain=forward src-address=192.168.77.0/24 dst-address=!10.5.8.0/24
```

**==> picture [13 x 13] intentionally omitted <==**

Split networking is not a security measure. The client (initiator) can still request a different Phase 2 traffic selector.
