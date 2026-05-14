## Create a route for each routing-mark 

```
add distance=1 dst-address=0.0.0.0/0 gateway=10.10.4.1
add distance=2 dst-address=0.0.0.0/0 gateway=10.10.5.1
```

To enable failover, it is necessary to have routes that will jump in as soon as others will become inactive on gateway failure. (and that will happen only if check-gateway option is active)
