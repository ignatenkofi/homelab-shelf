## `/interface ethernet switch acl` 

```
add action=drop src-mac-addr-state=sa-not-found src-ports=ether6,ether7 table=egress
add action=drop src-mac-addr-state=static-station-move src-ports=ether6,ether7 table=egress
```

CRS1xx/2xx switches also allow to learn one dynamic MAC per port to ensure only one end-user device is connected no matter its MAC address: 

```
/interface ethernet switch port
set ether6 learn-limit=1
set ether7 learn-limit=1
```
