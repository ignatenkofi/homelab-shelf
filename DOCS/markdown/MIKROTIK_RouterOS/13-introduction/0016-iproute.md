## `/ip/route` 

```
add dst-address=208.67.222.222 gateway=10.111.0.1 scope=10
add dst-address=208.67.220.220 gateway=10.112.0.1 scope=10
```

```
add distance=1 gateway=208.67.222.222 target-scope=11 check-gateway=ping
add distance=2 gateway=208.67.220.220 target-scope=11 check-gateway=ping
```

Essentially what it does is creates ECMP default route and if only one of the gateways is not reachable default route on the first link will still be active. Complete switchover to second link will happen only if all the gateways become unreachable. 

759
