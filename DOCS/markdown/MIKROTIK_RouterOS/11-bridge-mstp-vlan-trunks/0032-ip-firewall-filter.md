## `ip firewall filter` 

```
add chain=input connection-state=invalid action=drop comment="Drop Invalid connections"
```

```
add chain=input connection-state=established,related,untracked action=accept comment="Allow Established/Related
/Untracked connections
```

**==> picture [13 x 13] intentionally omitted <==**

Such a rule set must not be applied on routers with asymmetric routing, because asymmetrically routed packets may be considered invalid and dropped.
