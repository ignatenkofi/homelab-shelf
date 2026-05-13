## `/ip firewall filter` 

```
add action=accept chain=forward connection-state=established,related src-address=192.168.88.111
add action=accept chain=forward connection-state=established,related dst-address=192.168.88.111
add action=fasttrack-connection chain=forward connection-state=established,related hw-offload=no
add action=accept chain=forward connection-state=established,related
```

In this example, we exclude host 192.168.88.111, from being Fast-tracked, by first accepting it with the firewall rule, both for source and destination. The idea is - not allowing the traffic to reach the FastTrack action. 

Note: the "exclusion" rules, must be placed before fasttrack filters, order is important.
