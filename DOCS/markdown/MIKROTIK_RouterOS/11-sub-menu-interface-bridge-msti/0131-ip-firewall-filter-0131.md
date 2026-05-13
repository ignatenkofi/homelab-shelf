## `/ip firewall filter` 

```
add chain=forward action=fasttrack-connection connection-state=established,related \
  comment="fasttrack established/related"
```

```
add chain=forward action=accept connection-state=established,related \
  comment="accept established/related"
```

Notice that the first rule marks established/related connections as fast-tracked, the second rule is still required to accept packets belonging to those connections. The reason for this is that, as was mentioned earlier, some random packets from fast-tracked connections are still sent the slow pathway and only UDP and TCP are fast-tracked, but we still want to accept packets for other protocols. 

**==> picture [504 x 164] intentionally omitted <==**

**==> picture [504 x 207] intentionally omitted <==**

After adding the "FastTrack" rule special dummy rule appeared at the top of the list. This is not an actual rule, it is for visual information showing that some of the traffic is traveling FastPath and will not reach other firewall rules. 

693 

**==> picture [13 x 13] intentionally omitted <==**

FastTrack can process packets only in the main routing table so it is the system administrator duty to not FastTrack connections that are going through non-main routing table (thus connections that are processed with mangle action=mark-routing rules). Otherwise packets might be misrouted though the main routing table. 

These rules appear as soon as there is at least one fast-tracked connection tracking entry and will disappear after the last fast-tracked connection times out in the connection table. 

**==> picture [13 x 13] intentionally omitted <==**

The connection is FastTracked until a connection is closed, timed out or the router is rebooted.
