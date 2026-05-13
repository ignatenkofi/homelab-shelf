## `/routing/bgp/connection` 

```
add name=inst1_peer remote.address=192.168.1.1 as=1234 local.role=ebgp router-id=1.1.1.1
add name=inst2_peer remote.address=192.168.1.2 as=5678 local.role=ebgp router-id=2.2.2.2
```

When `router-id` is not specified BGP will pick the "default" ID from `/routing id` . 

**==> picture [13 x 13] intentionally omitted <==**

Starting from v7.20 instance is no longer determined by router-id.
