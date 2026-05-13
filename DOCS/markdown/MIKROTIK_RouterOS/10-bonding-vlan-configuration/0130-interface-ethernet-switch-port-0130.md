## `/interface ethernet switch port` 

```
set ether1,ether2,ether3 per-queue-scheduling="strict-priority:0,strict-priority:0,strict-priority:0,strict-
priority:0,strict-priority:0,strict-priority:0,strict-priority:0,strict-priority:0"
```

Map each PCP value to an internal priority value, for convenience reasons simply map PCP to an internal priority 1-to-1:
