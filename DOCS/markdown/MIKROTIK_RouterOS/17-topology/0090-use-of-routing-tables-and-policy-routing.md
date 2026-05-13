## Use of Routing Tables and Policy Routing 

The main difference from v6 is that the routing table must be added to the `/routing table` menu before actually referencing it anywhere in the configuration.  And fib parameter should be specified if the routing table is intended to push routes to the  FIB. The routing rule configuration is the same except for the menu location (instead of `/ip route rule` , now it is `/routing rule` ). 

Let's consider a basic example where we want to resolve 8.8.8.8 only in the routing table named myTable to the gateway 172.16.1.1: 

```
/routing table add name=myTable fib
/routing rule add dst-address=8.8.8.8 action=lookup-only-in-table table=myTable
/ip route add dst-address=8.8.8.8 gateway=172.16.1.1@main routing-table=myTable
```

Instead of routing rules, you could use mangle to mark packets with routing-mark, the same way as it was in ROSv6.
