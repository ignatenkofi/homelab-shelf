## The last two rules in mangle will simply mark all traffic from corresponding connections: 

```
add chain=forward action=mark-packet connection-mark=heavy_traffic_conn new-packet-mark=heavy_traffic
passthrough=no
```

```
add chain=forward action=mark-packet connection-mark=all_conn new-packet-mark=other_traffic passthrough=no
```
