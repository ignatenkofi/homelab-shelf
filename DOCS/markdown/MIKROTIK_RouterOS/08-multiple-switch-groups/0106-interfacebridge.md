## `/interface/bridge` 

```
set [find name=bridge] igmp-snooping=yes multicast-querier=yes query-interval=60s
```

```
/interface/bridge/port
set [find] fast-leave=yes
```
